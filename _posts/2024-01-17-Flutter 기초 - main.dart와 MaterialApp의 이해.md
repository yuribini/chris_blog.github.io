---
title: Flutter 기초 - main.dart와 MaterialApp의 이해
date: 2024-01-17 06:08:00 +09:00
categories: [Flutter, Flutter_Basic]
tags:
  [
    Flutter,
    Dart,
    Stateful Widget,
    State Management,
    UI Update,
    setState
  ]
---

![Flutter](/images/Flutter.png)


이 포스트에서는 Flutter 앱의 구조, `main.dart` 파일의 역할, `materialApp` 위젯의 중요성에 대한 내용을 작성하였다.<br>
<br>
<br>

## Flutter 앱의 시작점:`main.dart`
Dart 프로그램은 `main()` 함수에서 시작된다. Flutter 앱도 마찬가지로 `main.dart`파일이 entry point가 되고 앱의 전체적인 테마, 라우트 설정 등이 이루어지며, 이 파일에서 `runApp()`이 가장 중요한 함수가 된다.<Br>
<br>
<br>
<br>



## `runApp()` 함수의 역할 
`runApp()`함수는 Flutter 앱의 루트 위젯을 설정한다. 이 함수에 전달된 위젯은 앱의 최상위 위젯이 되며, 전체 앱UI의 기초가 된다. 일반적으로 `MaterialApp`, `CupertinoApp`, `WidgetsApp`의 인스턴스가 사용된다.
<Br>
<br>

> 인스턴스는 객체와 같은 의미로 사용되지만, 좀 더 구체적인 상황을 나타내는 데 사용된다. 클래스로부터 객체가 생성될 때, 그 객체를 인스턴스라고 부른다.

<Br>
<br>

```dart
void main() {
  runApp(MyApp());
}
```
여기서 `MyApp()`은 최상위 루트 위젯이다. 앱의 기본적인 스타일과 레이아웃을 설정한다.<br>
<br>
<br>

## `MaterialApp` 위젯의 중요성
`MaterialApp`위젯은 Flutter의 머터리얼 디자인 구현의 핵심이다. 이 위젯은 앱의 루트에 위치하며, 여러 중요한 기능과 속성을 제공한다.<br>
<br>

### 주요 속성 알아두기
- `title` : 앱의 이름을 정의
- `theme` : 전역적으로 적용되는 앱의 테마를 설정. 색상, 폰트 스타일 등
- `home` : 앱이 시작할 때 사용자에게 보여질 첫 화면을 지정
- `routes` : 앱의 다양한 화면 간 네비게이션 경로를 정의
- `initialRoute` : 초기에 보여질 화면의 경로를 지정
- `onGenerateRoute` : 동적으로 라우트를 생성할 때 사용되는 콜백
- `locale` & `localizationsDelegates` : 다국어 지원과 지역화를 위한 설정
- `debugShowCheckedModeBanner` : 개발 모드에서"Dubug"배너의 표시 여부 결정<br>
<br>

### `MaterialApp` 사용 예시
```dart
MaterialApp(
  title: '블라블라블라', // 앱의 타이틀 설정
  theme: ThemeData(
    primarySwatch: Colors.blue, // 앱의 기본 색상 테마 설정
  ),
  home: MyHomePage(), // 앱의 홈 화면 설정
  // 여기에 더 많은 설정을 추가할 수 있다....
)
```

<br>
<br>
<br>


Flutter는 모바일 앱 개발을 간소화하고, 빠르게 멋진 앱을 만들 수 있는 강력한 프레임워크이다. 특히 많은 부분이 간소화 되었기에 1인 개발에 좋은 프레임워크라고 생각한다. 내가 생각한 장점은 아래와 같다.

1. Flutter는 '모든 것이 위젯이다'라는 직관적이고 모듈화된 방식인 점
2. 단일 코드로 iOS & Android 앱을 동시에 개발할 수 있다는 점
3. 핫 리로드 기능으로 빠른 개발과 테스트가 가능하다는 점

이러한 장점들 때문에 나는 네이티브가 아닌 Flutter를 선택했고, 배워 나가고 있다.


