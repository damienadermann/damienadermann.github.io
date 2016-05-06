---
layout: post
title: "Mobile Development in 2016 is still broken"
date: "2016-05-07 09:02:30 +1000"
---

Lately I've had the oportunity to play around with a few of the newer alternatives for iOS/Android and its made me notice one problem that wasn't so obvious to me, mobile development today is still bad.

I've spent time over the years working on iOS apps in Xcode and have never had a problem. I actually really enjoy it. I enjoyed Objective-c and I enjoy swift. The IDE is great, the languages are well supported, the api is stable and well thought out, and the end result has usually been good apps. I have less experience with Android but to me it seems to be in a similar boat except less polished and has a big issue with lots device/os combinations to account for.

> It was 90% there but everytime some interaction lagged before responding a little part of me died

In the past two months I've worked on an app using [ionic 2](http://ionicframework.com/). I wasn't sure what to expect but having some experience with hybrid apps I was skeptical but excited. My first session learning and playing with ionic I was extremely impressed. Within an hour I had basic application structure set up and it looked native. The code was succinct and even elegant (which can't be said about obj-c and Java). The more I spent time using it the more I was impressed and excited. I spent my free time learning about [angular2](https://angular.io/)(the javascript framework ionic is built on) and listening to lots of podcasts. I was hooked. The biggest thing that impressed me was how well angular 2 was built for realtime UI programming. Its also improved so much since angular1. The use of [rxjs](https://github.com/Reactive-Extensions/RxJS) and redux(using [ngrx](https://github.com/ngrx/store)) gave me so much power in such a simple way I realised this had to be the future of Mobile development. And I think it is but its not the destination. That project has been stopped for now for 1 damning reason, while the app looked native, it didn't feel native. It was 90% there but everytime some interaction lagged before responding a little part of me died. I was so excited about the code but the results just weren't there, and I didn't want to admit it. I have no doubt that following this path will result in great apps but we are missing something at this stage.

> death to autolayout, all hail flexbox.

Mourning the loss of a new friend in Ionic I spent my bus trips to work searching for a new purpose in life. I stumbled across [React Native](https://facebook.github.io/react-native/). I had looked at RN while researching the feasability of Ionic but had dismissed it early thinking it was gimmicky and wouldn't give all the functionality a native app needs. Why would it, react was built as html view layer, how would that ever work in native land. Boy was I wrong. After watching the [React Native Fundamentals](https://egghead.io/series/react-native-fundamentals) series on egghead I was surprised. You could do a lot more than I thought so I tried an experiment. I spent a day porting over my existing unfinished swift sideproject into react native. The results I got out of that day were amazing. Not only did I get a lot done but the resulting app actually felt better than my swift app. The code was much smaller and simpler and app looked and felt great. So much so that I've ditched 6 or so weaks of work on my swift app to go with RN and I already feel that I've caught up and saved time by doing so. Also there is no compile time step when writing code. ReactNative has hot loading built in so writing code is much faster. I never noticed how much time I wasted waiting for the iOS simulator to fire up my app. Also death to autolayout, all hail flexbox.

> I don't think ReactNative as we see it today is the destination

React Native is young, not finished, [always changing](https://github.com/ericvicenti/navigation-rfc/blob/master/Docs/NavigationOverview.md) with a raw ecosystem around it but its the most all round native experience I've used. While the coding experience I'd argue isn't as polished as angular2 its simplicity is a huge asset and the react idea seems to be taking over the web world. I don't think ReactNative as we see it today is the destination for mobile development I think it the closest thing we have by a long shot. Another promising alternative is [Angular2 + Nativescript](https://www.youtube.com/watch?v=R3nyG2xtzeQ) but time will tell.

I'm now a ReactNative man. I recommend you try it too.
