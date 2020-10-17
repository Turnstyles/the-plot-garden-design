# Minimum Viable App Components and State

## Data

POJO: All possible cards, their associated text and types.

## Global State

currentTurn: Values: player1, player2... etc.

turnPhase: Values: otherPlayer, exploration, storytelling, etc.

Players: Values: necessary data for connection, current Hand contents, current Room location.

Map: Values: Graph, whose nodes are Rooms. Each room has Explored/Unexplored, Name, etc.

Story: Values: Array of objects, to keep chronological sequence. Each object has a Player reference (the one who wrote it) and a string (the actual story they wrote), Keywords that were relevant at time of writing, etc.

CardInPlay: Values: empty or Card

## App

Has Components: Hand, Map, Story, CardInPlay, Player2, Player3... (all except user-player, which is represented by Hand)

## Player2,3,etc.

Props: associated Player object

View: Just one card-back for each card in their hand.

## CardInPlay

Props: CardInPlay

View: Nothing, or, if CardInPlay exists, fixed-position Card display over top of Map.

## Hand

Props: Array of Cards (held in a property of the Player state)

Has Components: Cards, JSX map across array.

## Card (In Hand)

Props: Card text and types, shared via Context: turnPhase

Interactions: IF turnPhase=Exploration, Click Card to Play: Dispatch Action: turnPhase changes from Exploration to Storytelling.

## Map

Props: the Map graph, current Room location (property of Player object).

Has Components: Rooms.

## Room

Props: Room data (explored/unexplored, name, etc.), isOccupied, shared via Context: turnPhase

Interactions: IF turnPhase=Exploration Click Room to Explore: turnPhase changes from Exploration to Storytelling, player given random card that is IMMEDIATELY played.

## Story

Props: Story, turnPhase

Components: PastStory, CurrentStory

## PastStory

Props: Story

View: Just an scrollable text box, with a paragraph for each entry into the story so far, and a Player label at the top of the paragraph.

## CurrentStory

Props: turnPhase, cardInPlay

Has Components: EntryBox, ScribeButton

Interactions: Type into the textbox. When the textbox content matches via Regex with key words on cardInPlay, the Scribe button becomes clickable. Click Scribe Button: Dispatch Action: textbox content and player appended as object to Story array, and currentTurn rotates to next player.
