# CARD

## Data modeling
```mermaid
erDiagram
  CARD {
    id              integer   PK
    lesson_id       integer   FK
    front_text      text
    front_audio_uri text
  }

  WORD {
    id              integer   PK
    word            text
    definition      text
    phonetic        text
    part_of_speech  text
    audio_uri       text
    image_uri       text
  }

  CARD_WORD {
    card_id         integer   PK,FK
    word_id         integer   PK,FK
    word_order      integer         "Relative order of the word in the card."
  }

  CARD_WORD ||--o{ WORD : contains
  CARD_WORD ||--o{ CARD : contains
```

## Add card
+ add front text
  + the front text is added to `addCard` request body
+ select a word/phrase and mark it as new word
  + `#` is added on both sides of the word
  + the Suggestion List is shown below 
    + result populated with `searchWord` (full-text search)
    + search field can be edited
  + select one of the suggested words
    + the word is added to `addCard` request body
  + click the Add New Word
    + the Add New Word dialog is shown
    + enter word info and click Add
      + `createWord` is called
      + the word is added to `addCard` request body
+ upload front audio (optional)
  + `uploadAudio` is called
  + the audio_uri is added to `addCard` request body
+ click Add --> `addCard`
  + front text is Sanitize (e.g. html tags are not allowed) to prevent XSS, etc. 
  + `addWordToCard` is called
