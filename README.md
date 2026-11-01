# ScoreBoard (iOS)

A 2018 iOS app for NBA score-digit pools, the native predecessor of the Flutter [Scorbord](https://github.com/trey-a-hope/scorbord) prototype. A host posts a game with a buy-in price and a pot, players take a spot by picking the last digit of the home and away scores, pay with a card, and after the game the host evaluates the final score to settle it. Users can follow each other, message, and get push notifications.

## Features

- **Games**: list, add, update and view games (`GamesViewController`, `AddGameViewController`, `UpdateGameViewController`, `FullGameViewController`). A game (`Game.swift`) has home and away teams (`NBATeams.swift`) and scores, a start time, a pre/active/post status, a pot amount and a bet price.
- **Taking a spot**: `TakeGameViewController` lets a player choose a home digit and away digit (`Bet.swift`). `EvaluateGameViewController` settles a finished game.
- **Payments**: Stripe cards, payment methods and payment history (`PaymentMethodViewController`, `PaymentHistoryTableViewController`, `StripeApiClient.swift`). Stripe calls go through the PHP endpoint service at `es.tr3umphant-designs.com/assets/stripe` (see [endpoint-service.webiste](https://github.com/trey-a-hope/endpoint-service.webiste)).
- **Social**: profiles with photo cropping, followers and following, user search, messaging (JSQMessagesViewController) and notifications.
- **Account**: sign up, log in (email or Facebook), change email or password, settings, support, about, and an admin screen.

## How it works

The app is UIKit with storyboards (`Base.lproj/`) and XIB cells. Firebase handles Auth, Firestore (`MyFSRef.swift`), Storage and Cloud Messaging, configured by the committed `GoogleService-Info.plist`. `SessionManager.swift` keeps the signed-in user.

## Tech stack

- Swift, UIKit, CocoaPods
- Firebase (Auth, Core, Firestore, Messaging, Storage), Facebook Login, Stripe
- Alamofire, PromiseKit 4, Kingfisher 3, Material 2, JTAppleCalendar 7, JSQMessagesViewController, Google Maps, AKImageCropperView, EasyAnimation, Toaster, FontAwesome.swift

## Running it

The `Pods/` folder is committed, so you can open the workspace directly:

```sh
open ScoreBoard.xcworkspace
```

To refresh dependencies, run `pod install` first. Several pods are pinned to 2017-2018 major versions, so building with current Xcode will need dependency and Swift upgrades.

## Note

`AppDelegate.swift` and `StripeApiClient.swift` contain a Stripe test secret key. It's a test key, but it's still best to rotate it and keep secret keys off the device.
