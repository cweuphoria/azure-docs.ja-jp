---
title: "Azure Active Directory B2C: iOS アプリケーションを使用したトークンの取得 | Microsoft Docs"
description: "この記事では、Azure Active Directory B2C と AppAuth を使用してユーザー ID の管理とユーザーの認証を行う iOS アプリを作成する方法を説明します。"
services: active-directory-b2c
documentationcenter: ios
author: saeeda
manager: krassk
editor: 
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeeda
translationtype: Human Translation
ms.sourcegitcommit: c1cd1450d5921cf51f720017b746ff9498e85537
ms.openlocfilehash: 84f5ba5b3836f8524aafd9ca5e30978cc2702c1f
ms.lasthandoff: 03/14/2017


---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: iOS アプリケーションを使用してサインインする

Microsoft の ID プラットフォームには、OAuth2 や OpenID Connect といったオープンな標準が使用されています。 オープンな標準プロトコルを使用すると、開発者がサービスに統合するライブラリを選択する際の選択肢が増えます。 このチュートリアルも、他のチュートリアルと同じように、開発者が、Microsoft ID プラットフォームに接続するアプリケーションの記述を支援するために提供されています。 Microsoft の ID プラットフォームには、[RFC6749 OAuth2 仕様](https://tools.ietf.org/html/rfc6749)を実装するほとんどのライブラリから接続できます。

> [!WARNING]
> Microsoft では、サード パーティ製のライブラリ用の修正プログラムは提供していません。また、これらのライブラリのレビューも実施していません。 このサンプルでは、Azure AD B2C を使用する基本的なシナリオでの互換性がテスト済みである、AppAuth と呼ばれるサード パーティ製のライブラリを使用しています。 問題や機能に関する要望は、ライブラリのオープン ソース プロジェクトにお送りください。 詳細については、 [こちらの記事](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries)を参照してください。
>
>

ここで紹介する構成サンプルは OAuth2 や OpenID Connect に精通している読者を想定しており、それ以外の方にとっては、あまり参考にならない可能性があります。 その場合は、 [対応プロトコルについて簡単に解説したこちらの記事](active-directory-b2c-reference-protocols.md)に目を通すことをお勧めします。

Azure Active Directory のシナリオおよび機能のすべてが B2C プラットフォームでサポートされているわけではありません。  B2C プラットフォームを使用する必要があるかどうかを判断するには、 [B2C の制限事項](active-directory-b2c-limitations.md)に関するページをお読みください。

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C ディレクトリの取得
Azure AD B2C を使用するには、ディレクトリ (つまり、テナント) を作成しておく必要があります。 ディレクトリは、ユーザー、アプリ、グループなどをすべて格納するためのコンテナーです。 まだディレクトリを作成していない場合は、 [B2C ディレクトリを作成](active-directory-b2c-get-started.md) してから先に進んでください。

## <a name="create-an-application"></a>アプリケーションの作成
次に、B2C ディレクトリにアプリを作成する必要があります。 アプリを登録すると、Azure AD がアプリと安全に通信するために必要な情報が提供されます。 モバイル アプリを作成するには、[こちらの手順](active-directory-b2c-app-registration.md)に従ってください。 次を行ってください。

* **モバイル デバイス** をアプリケーションに含めます。
* アプリに割り当てられた **アプリケーション ID** をコピーしておきます。 この GUID は後で必要になります。
* カスタム スキーマを使用する**リダイレクト URI** を設定します (例: com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)。 この URI は後で必要になります。

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>ポリシーの作成
Azure AD B2C では、すべてのユーザー エクスペリエンスが [ポリシー](active-directory-b2c-reference-policies.md)によって定義されます。 このアプリには、サインインとサインアップを組み合わせた&1; つの ID エクスペリエンスが含まれています。 [ポリシーについてのリファレンス記事](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)で説明されているように、このポリシーを作成する必要があります。 ポリシーを作成するときは、以下の操作を必ず実行してください。

* ポリシーで、 **[表示名]** とサインアップ属性を選択します。
* すべてのポリシーで、アプリケーション要求として **[表示名]** と **[オブジェクト ID]** を選択します。 その他のクレームも選択できます。
* ポリシーの作成後、各ポリシーの **名前** をコピーしておきます。 名前には、 `b2c_1_`というプレフィックスが付加されています。  このポリシー名は後で必要になります。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

ポリシーを作成したら、アプリを構築できます。

## <a name="download-the-sample-code"></a>サンプル コードのダウンロード
AppAuth と Azure AD B2C を使用する実稼働するサンプルが [github](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c) に用意されています。 そのコードをダウンロードして実行できます。 独自の Azure AD B2C テナントを使用するには、[README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) の指示に従います。

このサンプルは、[GitHub の iOS AppAuth プロジェクト](https://github.com/openid/AppAuth-iOS)の README の指示に従って作成されています。 サンプルとライブラリの動作の詳細については、GitHub の AppAuth README を参照します。

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a>Azure AD と B2C AppAuth を使用するようにアプリを変更する

> [!NOTE]
> AppAuth は、サポート iOS 7 以降をサポートします。  ただし、Google でのソーシャル ログインをサポートするには SFSafariViewController が必要であり、iOS 9 以降が必要です。
>

### <a name="configuration"></a>構成

Azure AD B2C との通信は、承認エンドポイント URI とトークン エンドポイント URI の両方を指定することで構成できます。  これらの URI を生成するには、次の情報が必要です。
* テナント ID (例: contoso.onmicrosoft.com)
* ポリシー名 (例: B2C\_1\_SignUpIn)

トークン エンドポイント URI は、次の URL の Tenant\_ID と Policy\_Name を置き換えることで生成できます。

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

承認エンドポイント URI は、次の URL の Tenant\_ID と Policy\_Name を置き換えることで生成できます。

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

AuthorizationServiceConfiguration オブジェクトを作成するには、次のコードを実行します。

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a>承認

承認サービスの構成を行うか取得した後、承認要求を構築できます。 この要求を作成するには、次の情報が必要です。  
* クライアント ID (例: 00000000-0000-0000-0000-000000000000)
* カスタム スキーマを使用するリダイレクト URI (例: com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

どちらの項目も、[アプリの登録](#create-an-application)を行ったときに保存されています。

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

カスタム スキームを使用する URI へのリダイレクトを処理するようにアプリケーションを設定するには、Info.pList の 'URL スキーム' の一覧をを更新する必要があります。
* Info.pList を開きます。
* 'Bundle creator OS Type Code' のような行の上にマウス ポインタ―を置き、\+ 記号をクリックします。
* 新しい行の 'URL types' の名前を変更します。
* 'URL types' の左側にある矢印をクリックします。
* Item 0 の値の名前を 'URL Schemes' に変更します。
* 'URL Schemes' の下の 'Item 0' の値を編集して、アプリケーションの一意のスキーマの値を設定します。  OIDAuthorizationRequest オブジェクトの作成時の redirectURL のスキームと一致させる必要があります。
* この例では、''com.onmicrosoft.fabrikamb2c.exampleapp' スキームを使用しています。

残りのプロセスを完了する方法については、[AppAuth ガイド](https://openid.github.io/AppAuth-iOS/)を参照してください。 動作するアプリをすぐに開始する必要がある場合は、[用意されているサンプル](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c)をチェックしてください。 [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) の手順に従って、独自の Azure AD B2C 構成を入力してください。

ご意見とご提案をお待ちしております。 このトピックに問題がある場合、またはこのコンテンツを改善するためのご提案がある場合には、ページの下部でフィードバックを送信できます。 機能についてのご要望は、[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) までお寄せください。

