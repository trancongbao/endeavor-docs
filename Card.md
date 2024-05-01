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
+ Add front text. 
+ Select a word/phrase and mark it as new word
  + `#` is added on both sides of the word
  + suggestions dialog is shown with result populated with `searchWord`
  + show  (full-text search), search field can be edited.
+ Select one of the suggested words --> `addWordToCard`
+ Select Add Word instead --> Add Word Dialog --> `createWord`
+ Optional: upload front audio
+ Click create --> `createCard`
    + Sanitize front text to prevent XSS, etc: html tags are not allowed.
