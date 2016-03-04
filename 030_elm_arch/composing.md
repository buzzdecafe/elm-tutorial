# Composing

One of the big benefits from using the Elm architecture is the way it handles composition of components. To understand this let's build an example:

- We will have a parent component `App`
- And a child component `Widget`

This is the code for the __Widget.elm__ component:

```elm
module C030ElmArch.Composing.Widget (..) where

import Html exposing (Html)
import Html.Events as Events


-- MODEL


type alias Model =
  { count : Int
  }


type Action
  = Increase


initialModel : Model
initialModel =
  { count = 0
  }



-- VIEW


view : Signal.Address Action -> Model -> Html
view address model =
  Html.div
    []
    [ Html.div [] [ Html.text (toString model.count) ]
    , Html.button
        [ Events.onClick address Increase
        ]
        [ Html.text "Click" ]
    ]



-- UPDATE


update : Action -> Model -> Model
update action model =
  case action of
    Increase ->
      { model | count = model.count + 1 }
```
