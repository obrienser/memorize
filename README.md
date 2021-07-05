# Memorize Game :video_game:
###### Stanford University's course CS193p (Developing Applications for iOS using SwiftUI)

[![GitHub license](https://img.shields.io/github/license/obrienser/Memorize)](https://github.com/obrienser/Memorize/blob/main/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/obrienser/Memorize)](https://github.com/obrienser/Memorize/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/obrienser/Memorize)](https://github.com/obrienser/Memorize/network)
[![visitors](https://visitor-badge.glitch.me/badge?page_id=obrienser.Memorize)](https://github.com/obrienser)

<br>
<br>
<p align="center">
  <img src="/Screenshots/screencast.gif" alt="" width="600" align="middle">
</p>
<br>

## About the game
You need to turn over the cards one by one to find the same cards. When you **find two identical cards,** you get one point and these cards will disappear. The game ends when you **find all the pairs.**

## Technology
* Swift
* SwiftUI
* MVVM

## Screenshots

<p align="center">
  <img src="/Screenshots/01.png" alt="" height="450"> &nbsp;&nbsp;<img src="/Screenshots/02.png" alt="" height="450"> &nbsp;&nbsp;<img src="/Screenshots/03.png" alt="" height="450"> &nbsp;&nbsp;<img src="/Screenshots/04.png" alt="" height="450">
</p>

## Sample code
>MemoryGame.swift

```swift
    struct Card: Identifiable {
        var isFaceUp: Bool = false {
            didSet {
                if isFaceUp {
                    startUsingBonusTime()
                } else {
                    stopUsingBonusTime()
                }
            }
        }
        var isMatched: Bool = false {
            didSet {
                stopUsingBonusTime()
            }
        }
        var content: CardContent
        var id: Int
        
        // can be zero which means "no bonus available" for this card
        var bonusTimeLimit: TimeInterval = 10
        
        // how long this card has ever been face up
        private var faceUpTime: TimeInterval {
            if let lastFaceUpDate = self.lastFaceUpDate {
                return pastFaceUpTime + Date().timeIntervalSince(lastFaceUpDate)
            } else {
                return pastFaceUpTime
            }
        }
        // the last time this card was turned face up (and is still face up)
        var lastFaceUpDate: Date?
        // the accumulated  time yhis card has been face up in the past
        // (i.e. not including the current time it`s been face up if it is currently so)
        var pastFaceUpTime: TimeInterval = 0
        
        // how much time left before the bonus opportunity runs out
        var bonusTimeRemaining: TimeInterval {
            max(0, bonusTimeLimit - faceUpTime)
        }
        // percentage of the bonus time remaining
        var bonusRemaining: Double {
            (bonusTimeLimit > 0 && bonusTimeRemaining > 0) ? bonusTimeRemaining/bonusTimeLimit : 0
        }
        // whether the card was matched during the bonus time period
        var hasEarnedBonus: Bool {
            isMatched && bonusTimeRemaining > 0
        }
        // whether we are currently face up, unmatched and have not yet used up the bonus window
        var isConsumingBonusTime: Bool {
            isFaceUp && !isMatched && bonusTimeRemaining > 0
        }
        
        // called when the card transitions to face up state
        private mutating func startUsingBonusTime() {
            if isConsumingBonusTime, lastFaceUpDate == nil {
                lastFaceUpDate = Date()
            }
        }
        // called when the card goes back face down (or gets matched)
        private mutating func stopUsingBonusTime() {
            pastFaceUpTime = faceUpTime
            self.lastFaceUpDate = nil
        }
    }
```

## About the course
Stanford's CS193p course, Developing Applications for iOS, explains the fundamentals of how to build applications for iPhone and iPad using SwiftUI.

>[Stanford University's course CS193p (Developing Applications for iOS using SwiftUI)](https://cs193p.sites.stanford.edu/2020)

### Lectures
1. Course Logistics and Intro to SwiftUI
2. MVVM and the Swift Type System
3. Reactive UI Protocols Layout
4. Grid enum Optionals
5. ViewBuilder Shape ViewModifier
6. Animation
7. Multithreading EmojiArt
8. Gestures JSON
9. Data Flow
10. Modal Presentation and Navigation
11. Enroute Picker
12. Core Data
13. Persistence
14. UIKit Integration

## Requirements
* iOS 14.2
* Xcode 12.0
* Swift 5.3

## Install
Just open project and run :rocket:

<br>
<p align="center">
  <a href="https://www.buymeacoffee.com/obrienser">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" width="140">
  </a>
</p>
