---
tags:
  - program
  - 未共有
source: https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide
---
この JavaScript ガイドでは、[JavaScript](https://developer.mozilla.org/ja/docs/Web/JavaScript) の使い方を紹介し、この言語の概要を説明します。言語機能についてもっと知りたい場合は、[JavaScript リファレンス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference)を参照してください。
## In this article
- [入門編](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%85%A5%E9%96%80%E7%B7%A8)
- [文法とデータ型](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%96%87%E6%B3%95%E3%81%A8%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B)
- [制御フローとエラー処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%88%B6%E5%BE%A1%E3%83%95%E3%83%AD%E3%83%BC%E3%81%A8%E3%82%A8%E3%83%A9%E3%83%BC%E5%87%A6%E7%90%86)
- [ループと反復処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%AB%E3%83%BC%E3%83%97%E3%81%A8%E5%8F%8D%E5%BE%A9%E5%87%A6%E7%90%86)
- [関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E9%96%A2%E6%95%B0)
- [式と演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%BC%8F%E3%81%A8%E6%BC%94%E7%AE%97%E5%AD%90)
- [数値と文字列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%95%B0%E5%80%A4%E3%81%A8%E6%96%87%E5%AD%97%E5%88%97)
- [日付と時刻の表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%97%A5%E4%BB%98%E3%81%A8%E6%99%82%E5%88%BB%E3%81%AE%E8%A1%A8%E7%8F%BE)
- [正規表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)
- [インデックス付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%A4%E3%83%B3%E3%83%87%E3%83%83%E3%82%AF%E3%82%B9%E4%BB%98%E3%81%8D%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)
- [キー付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AD%E3%83%BC%E4%BB%98%E3%81%8D%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)
- [オブジェクトの操作](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E6%93%8D%E4%BD%9C)
- [クラスの使用](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AF%E3%83%A9%E3%82%B9%E3%81%AE%E4%BD%BF%E7%94%A8)
- [プロミス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%97%E3%83%AD%E3%83%9F%E3%82%B9)
- [型付き配列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%9E%8B%E4%BB%98%E3%81%8D%E9%85%8D%E5%88%97)
- [イテレーターとジェネレーター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%A4%E3%83%86%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC%E3%81%A8%E3%82%B8%E3%82%A7%E3%83%8D%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC)
- [国際化](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%9B%BD%E9%9A%9B%E5%8C%96)
- [メタプログラミング](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%A1%E3%82%BF%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0)
- [JavaScript モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#javascript_%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB)

## [入門編](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%85%A5%E9%96%80%E7%B7%A8)

概要: [入門編](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction)

- [このガイドについて](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#javascript_%E3%81%AE%E6%83%85%E5%A0%B1%E3%81%AF%E3%81%A9%E3%81%93%E3%81%AB%E3%81%82%E3%82%8B%E3%81%8B)
- [JavaScript について](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#javascript_%E3%81%A8%E3%81%AF%E4%BD%95%E3%81%8B)
- [JavaScript と Java](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#javascript_%E3%81%A8_java)
- [ECMAScript](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#javascript_%E3%81%A8_ecmascript_%E4%BB%95%E6%A7%98%E6%9B%B8)
- [ツール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#javascript_%E3%82%92%E5%A7%8B%E3%82%81%E3%82%88%E3%81%86)
- [Hello World](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Introduction#hello_world)

## [文法とデータ型](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%96%87%E6%B3%95%E3%81%A8%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B)

概要: [文法とデータ型](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types)

- [基本構文とコメント](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%9F%BA%E6%9C%AC)
- [宣言](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%AE%A3%E8%A8%80)
- [変数のスコープ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%A4%89%E6%95%B0%E3%81%AE%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97)
- [変数の巻き上げ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E5%A4%89%E6%95%B0%E3%81%AE%E5%B7%BB%E3%81%8D%E4%B8%8A%E3%81%92)
- [データ構造とデータ型](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E3%83%87%E3%83%BC%E3%82%BF%E6%A7%8B%E9%80%A0%E3%81%A8%E3%83%87%E3%83%BC%E3%82%BF%E5%9E%8B)
- [リテラル](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Grammar_and_types#%E3%83%AA%E3%83%86%E3%83%A9%E3%83%AB)

## [制御フローとエラー処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%88%B6%E5%BE%A1%E3%83%95%E3%83%AD%E3%83%BC%E3%81%A8%E3%82%A8%E3%83%A9%E3%83%BC%E5%87%A6%E7%90%86)

概要: [制御フローとエラー処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)

- [`if...else`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#if...else_%E6%96%87)
- [`switch`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#switch_%E6%96%87)
- [`try`/`catch`/`throw`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#%E4%BE%8B%E5%A4%96%E5%87%A6%E7%90%86%E6%96%87)
- [エラーオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Control_flow_and_error_handling#error_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E6%B4%BB%E7%94%A8)

## [ループと反復処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%AB%E3%83%BC%E3%83%97%E3%81%A8%E5%8F%8D%E5%BE%A9%E5%87%A6%E7%90%86)

概要: [ループと反復処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration)

- [`for`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#for_%E6%96%87)
- [`while`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#while_%E6%96%87)
- [`do...while`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#do...while_%E6%96%87)
- [`continue`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#continue_%E6%96%87)
- [`break`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#break_%E6%96%87)
- [`for..in`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#for...in_%E6%96%87)
- [`for..of`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Loops_and_iteration#for...of_%E6%96%87)

## [関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E9%96%A2%E6%95%B0)

概要: [関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions)

- [関数の定義](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E9%96%A2%E6%95%B0%E3%81%AE%E5%AE%9A%E7%BE%A9)
- [関数の呼び出し](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E9%96%A2%E6%95%B0%E3%81%AE%E5%91%BC%E3%81%B3%E5%87%BA%E3%81%97)
- [関数のスコープ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E9%96%A2%E6%95%B0%E3%81%AE%E3%82%B9%E3%82%B3%E3%83%BC%E3%83%97)
- [クロージャ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E3%82%AF%E3%83%AD%E3%83%BC%E3%82%B8%E3%83%A3)
- [実引数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#arguments_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E4%BD%BF%E7%94%A8) と [仮引数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E9%96%A2%E6%95%B0%E3%81%AE%E5%BC%95%E6%95%B0)
- [アロー関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions#%E3%82%A2%E3%83%AD%E3%83%BC%E9%96%A2%E6%95%B0)

## [式と演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%BC%8F%E3%81%A8%E6%BC%94%E7%AE%97%E5%AD%90)

概要: [式と演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators)

- [代入演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E4%BB%A3%E5%85%A5%E6%BC%94%E7%AE%97%E5%AD%90) と [比較演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E6%AF%94%E8%BC%83%E6%BC%94%E7%AE%97%E5%AD%90)
- [算術演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E7%AE%97%E8%A1%93%E6%BC%94%E7%AE%97%E5%AD%90)
- [ビット演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E3%83%93%E3%83%83%E3%83%88%E6%BC%94%E7%AE%97%E5%AD%90) と [論理演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E8%AB%96%E7%90%86%E6%BC%94%E7%AE%97%E5%AD%90)
- [条件演算子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Expressions_and_operators#%E6%9D%A1%E4%BB%B6%EF%BC%88%E4%B8%89%E9%A0%85%EF%BC%89%E6%BC%94%E7%AE%97%E5%AD%90)

## [数値と文字列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%95%B0%E5%80%A4%E3%81%A8%E6%96%87%E5%AD%97%E5%88%97)

概要: [数値と文字列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings)

- [数値リテラル](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#%E6%95%B0%E5%80%A4)
- [`Number` オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#number_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [`Math` オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#math_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [文字列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#%E6%96%87%E5%AD%97%E5%88%97)
- [`String` オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#string_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [テンプレートリテラル](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Numbers_and_strings#%E3%83%86%E3%83%B3%E3%83%97%E3%83%AC%E3%83%BC%E3%83%88%E3%83%AA%E3%83%86%E3%83%A9%E3%83%AB)

## [日付と時刻の表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%97%A5%E4%BB%98%E3%81%A8%E6%99%82%E5%88%BB%E3%81%AE%E8%A1%A8%E7%8F%BE)

概要: [日付と時刻の表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Representing_dates_times)

- [`Date` オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Representing_dates_times#date_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

## [正規表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE)

概要: [正規表現](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions)

- [正規表現の作成](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions#%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE%E3%81%AE%E4%BD%9C%E6%88%90)
- [正規表現パターンの記述](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions#%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE%E3%83%91%E3%82%BF%E3%83%BC%E3%83%B3%E3%81%AE%E8%A8%98%E8%BF%B0)
    - [アサーション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions/Assertions)
    - [文字クラス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions/Character_classes)
    - [グループと後方参照](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions/Groups_and_backreferences)
    - [数量子](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Regular_expressions/Quantifiers)

## [インデックス付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%A4%E3%83%B3%E3%83%87%E3%83%83%E3%82%AF%E3%82%B9%E4%BB%98%E3%81%8D%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)

概要: [インデックス付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Indexed_collections)

## [キー付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AD%E3%83%BC%E4%BB%98%E3%81%8D%E3%82%B3%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)

概要: [キー付きコレクション](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Keyed_collections)

- [`Map`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Keyed_collections#map_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [`WeakMap`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Keyed_collections#weakmap_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [`Set`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Keyed_collections#set_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [`WeakSet`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Keyed_collections#weakset_%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

## [オブジェクトの操作](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E6%93%8D%E4%BD%9C)

概要: [オブジェクトを利用する](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_objects)

- [オブジェクトとそのプロパティ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_objects#%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%A8%E3%83%97%E3%83%AD%E3%83%91%E3%83%86%E3%82%A3)
- [新しいオブジェクトの作成](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_objects#%E6%96%B0%E3%81%97%E3%81%84%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%81%AE%E4%BD%9C%E6%88%90)
- [メソッドの定義](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_objects#%E3%83%A1%E3%82%BD%E3%83%83%E3%83%89%E3%81%AE%E5%AE%9A%E7%BE%A9)
- [ゲッターとセッター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Working_with_objects#%E3%82%B2%E3%83%83%E3%82%BF%E3%83%BC%E3%81%A8%E3%82%BB%E3%83%83%E3%82%BF%E3%83%BC%E3%81%AE%E5%AE%9A%E7%BE%A9)

## [クラスの使用](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%AF%E3%83%A9%E3%82%B9%E3%81%AE%E4%BD%BF%E7%94%A8)

概要: [オブジェクトモデルの詳細](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_classes)

- [クラスの宣言](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_classes#%E3%82%AF%E3%83%A9%E3%82%B9%E3%81%AE%E5%AE%A3%E8%A8%80)
- [さまざまなクラス機能](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_classes#%E3%82%B3%E3%83%B3%E3%82%B9%E3%83%88%E3%83%A9%E3%82%AF%E3%82%BF%E3%83%BC)
- [拡張と継承](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_classes#%E6%8B%A1%E5%BC%B5%E3%81%A8%E7%B6%99%E6%89%BF)
- [なぜクラスか](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_classes#%E3%81%AA%E3%81%9C%E3%82%AF%E3%83%A9%E3%82%B9%E3%81%8B)

## [プロミス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%97%E3%83%AD%E3%83%9F%E3%82%B9)

概要: [プロミス](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises)

- [保証](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises#%E4%BF%9D%E8%A8%BC)
- [チェーン](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises#%E9%80%A3%E9%8E%96)
- [エラーの処理](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises#%E3%82%A8%E3%83%A9%E3%83%BC%E5%87%A6%E7%90%86)
- [合成](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises#%E5%90%88%E6%88%90)
- [タイミング](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises#%E3%82%BF%E3%82%A4%E3%83%9F%E3%83%B3%E3%82%B0)

## [型付き配列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%9E%8B%E4%BB%98%E3%81%8D%E9%85%8D%E5%88%97)

概要: [型付き配列](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Typed_arrays)

## [イテレーターとジェネレーター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%82%A4%E3%83%86%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC%E3%81%A8%E3%82%B8%E3%82%A7%E3%83%8D%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC)

概要: [イテレーターとジェネレーター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_generators)

- [イテレーター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_generators#%E3%82%A4%E3%83%86%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC)
- [反復可能オブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_generators#%E5%8F%8D%E5%BE%A9%E5%8F%AF%E8%83%BD%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)
- [ジェネレーター](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Iterators_and_generators#%E3%82%B8%E3%82%A7%E3%83%8D%E3%83%AC%E3%83%BC%E3%82%BF%E3%83%BC%E9%96%A2%E6%95%B0)

## [国際化](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E5%9B%BD%E9%9A%9B%E5%8C%96)

概要: [国際化](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Internationalization)

- [日付と時刻の整形](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Internationalization#%E6%97%A5%E4%BB%98%E3%81%A8%E6%99%82%E5%88%BB%E3%81%AE%E6%9B%B8%E5%BC%8F%E5%8C%96)
- [数値の整形](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Internationalization#%E6%95%B0%E5%80%A4%E3%81%AE%E6%9B%B8%E5%BC%8F%E5%8C%96)
- [照合](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Internationalization#%E7%85%A7%E5%90%88)

## [メタプログラミング](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#%E3%83%A1%E3%82%BF%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%9F%E3%83%B3%E3%82%B0)

概要: [メタプログラミング](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Meta_programming)

- [`Proxy`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Meta_programming#%E3%83%97%E3%83%AD%E3%82%AD%E3%82%B7%E3%83%BC)
- [ハンドラーとトラップ](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Meta_programming#%E3%83%8F%E3%83%B3%E3%83%89%E3%83%A9%E3%83%BC%E3%81%A8%E3%83%88%E3%83%A9%E3%83%83%E3%83%97)
- [取り消し可能プロキシー](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Meta_programming#%E5%8F%96%E3%82%8A%E6%B6%88%E3%81%97%E5%8F%AF%E8%83%BD_proxy)
- [`Reflect`](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Meta_programming#%E3%83%AA%E3%83%95%E3%83%AC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)

## [JavaScript モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide#javascript_%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB)

概要: [JavaScript モジュール](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules)

- [エクスポート](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E6%A9%9F%E8%83%BD%E3%81%AE%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88)
- [インポート](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88%E3%81%B8%E3%81%AE%E6%A9%9F%E8%83%BD%E3%81%AE%E3%82%A4%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%88)
- [デフォルトエクスポート](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%81%A8%E5%90%8D%E5%89%8D%E4%BB%98%E3%81%8D%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88)
- [名前を変更する](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E3%82%A4%E3%83%B3%E3%83%9D%E3%83%BC%E3%83%88%E3%82%84%E3%82%A8%E3%82%AF%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%81%AE%E5%90%8D%E5%89%8D%E3%82%92%E5%A4%89%E6%9B%B4%E3%81%99%E3%82%8B)
- [モジュールの集約](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%AE%E9%9B%86%E7%B4%84)
- [動的なモジュールの読み込み](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Modules#%E5%8B%95%E7%9A%84%E3%81%AA%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%81%AE%E8%AA%AD%E3%81%BF%E8%BE%BC%E3%81%BF)