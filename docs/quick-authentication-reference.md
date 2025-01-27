# Microsoft Quick Authentication configuration and JavaScript API reference

These settings and APIs allow you to customize the appearance and behavior of the UI provided by Microsoft Quick Authentication.

For information about how to use Quick Authentication, see the [Sign in Microsoft account users to a single-page app (SPA) with Microsoft Quick Authentication](./quick-authentication-how-to.md).

> Microsoft Quick Authentication is in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Some features might be unsupported or have constrained capabilities. For more information, see [Supplemental terms of use for Microsoft Azure previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).

## Logging with autoLogEvents

The `autoLogEvents` query parameter supports these log level values:

- `0`: Log only error events.
- `1`: Log only error and warning events.
- `2`: Log error, warning and information events.

## MSAL Logging with logMsalEvents

Quick Authentication is built on top of [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser). MSAL.js logging to console can also be enabled using `logMsalEvents` query parameter.

The `logMsalEvents` query parameter supports MSAL [log levels](https://azuread.github.io/microsoft-authentication-library-for-js/ref/enums/_azure_msal_common.loglevel.html):

- `0`: Error.
- `1`: Warning.
- `2`: Info
- `3`: Verbose.
- `4`: Trace.

`autoLogEvents` needs to be set (can be any value) for `logMsalEvents` take effect.

## Customizing the sign-in prompt

You can customize the setup of the Quick Authentication sign-in prompt using a handful of options. These values are supplied as part of the initialization object in your JavaScript or as data attributes in the initialization `div` in your HTML (prefixed with `data-`):

| Property                | Values                             | Default  |
|-------------------------|------------------------------------|----------|
| `auto_prompt`           | `true` or `false`                  | `true`   |
| `auto_sign_in`          | `true` or `false`                  | `false`  |
| `context`               | "signin"<br/> "signup"<br/> "use"  | "signin" |
| `cancel_on_tap_outside` | `true` or `false`                  | `true`   |
| `prompt_position`       | "left"<br/> "center"<br/> "right"  | "left"   |

### `auto_prompt`

Controls whether the one-tap prompt should show up. Only shows for MSA profiles in Microsoft Edge.

### `auto_sign_in`

Only applicable when `auto_prompt` is `true`. If set to `true`, it will complete the sign-in automatically, without the user needing to do anything.

### `context`

Defines the text variant to be used in the prompt.

- "signin" = "Sign in with Microsoft" (default)
- "signup" = "Sign up with Microsoft"
- "use" = "Use Microsoft"

### `cancel_on_tap_outside`

Whether to close the prompt when a user moves focus out of the prompt.

### `prompt_position`

Controls the rendering location of the prompt in Microsoft Edge. Choosing "right" will anchor it to the user's Edge profile's avatar button.

## Customizing the sign-in button

You can customize the look and feel of the sign-in button using a handful of options. These values are supplied as part of the `renderSignInButton()` call in your JavaScript or as data attributes on the button container `div` in your HTML (prefixed with `data-`):

| Property         | Values                                                              | Default       |
|------------------|---------------------------------------------------------------------|---------------|
| `type`           | "standard"<br/> "icon"                                              | "standard"    |
| `theme`          | "dark"<br/> "light"                                                 | "dark"        |
| `size`           | "small"<br/> "medium"<br/> "large"                                  | "large"       |
| `text`           | "signin_with"<br/> "signup_with"<br/> "continue_with"<br/> "signin" | "signin_with" |
| `shape`          | "rectangular"<br/> "rounded"<br/> "pill"                            | "rectangular" |
| `width`          | number in CSS pixels<br/> 200–600                                   |               |
| `height`         | number in CSS pixels<br/> 24–100                                    |               |
| `logo_alignment` | "left"<br/> "center"                                                | "left"        |

### `type`

| standard (default)                                                                                                                                                                                                                                        | icon                                                                                         |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|
| ![The standard button type is full width, with text](./media/standard.png)<br/> ![When we know the user's identity, the standard button will include their avatar, name, and email](./media/standard-known.png) | ![The icon button type only shows the Microsoft icon](./media/icon.png) |

### `theme`

| dark (default)                                                                                                                                                                                                                                | light                                                                                                                                                                                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![The dark button theme is a dark button with light text](./media/standard.png)<br/> ![The dark version of the known user button with a dark background and light text](./media/standard-known.png) | ![The light button theme is a light button with dark text](./media/light.png)<br/> ![The light version of the known user button with a light background and dark text](./media/light-known.png) |

### `size`

| small (28 px) | medium (36 px) | large (42 px - default) |
|---------|---------|---------|
| ![The small button is 28 px high](./media/small.png)<br/> ![The small version of the known user button does not include the user's email](./media/small-known.png) | ![The small button is 36 px high](./media/standard.png)<br/> ![The medium version of the known user button](./media/standard-known.png) | ![The large button is 42 px high](./media/large.png)<br/> ![The large version of the known user button includes larger text and avatar](./media/large-known.png) |

### `text`

The `text` property governs the text shown in sign-in button. Other properties affect what is finally shown as mentioned in table below.

| Text            | `standard` button         | `icon` button | `standard` button in Microsoft Edge MSA profile |
|-----------------|---------------------------|---------------|-------------------------------------------------|
| `signin_with`   | "Sign in with Microsoft"  | None          | "Sign in as Grant"                              |
| `signup_with`   | "Sign up with Microsoft"  | None          | "Sign up as Grant"                              |
| `continue_with` | "Continue with Microsoft" | None          | "Continue as Grant"                             |
| `signin`        | "Sign in"                 | None          | "Sign in as Grant"                              |

In above table, we assume "Grant Zander" is user signed into MSA profile in Microsoft Edge.

### `shape`

| rectangular (default) | rounded | pill |
|---------|---------|---------|
| ![The rectangular button shape has no border radius](./media/standard.png)<br/> | ![The rounded button shape has a slight border radius](./media/rounded.png) | ![The pill button shape has sides that are half-circles](./media/pill.png)<br/> ![The pill version of the known user button nestles the avatar into the semi-circle](./media/pill-known.png) |

### `logo_alignment`

| left | center (default) |
|---------|---------|
| ![The left logo alignment has the logo and text aligned to the left of the button](./media/left.png) | ![The center logo alignment has the logo and text aligned to the center of the button](./media/standard.png) |

## JavaScript API reference - Microsoft Quick Authentication

## Data Type: InitConfiguration

`InitConfiguration` is the configuration object that needs to be passed as argument to [ms.auth.initialize](#method-msauthinitialize) method.

| Property                | Value(s)                                                                      | Default value                 | Required | More info                                                                                           |
|-------------------------|:------------------------------------------------------------------------------|:-----------------------------:|----------|-------------------------------------------------------------------------------------------------------|
| `client_id`             | **Application (client) ID**                                                   | (no default value)            | Yes      | See [Register your application](quick-authentication-how-to.md#register-your-application).   |
| `login_uri`             | **Redirect URI**                                                              | _https://<domain>/blank.html_ | No       | See [Register your application](quick-authentication-how-to.md#register-your-application).                                                                                                      |
| `callback`              | JavaScript function that receives account information once sign-in completes. | (no default value)            | Yes      | On successful sign-in, this function is called with the [SignInAccountInfo](#data-type-signinaccountinfo) object. |
| `auto_prompt`           | `true` or `false`                                                             | `true`                        | No       |                                                                                                       |
| `auto_sign_in`          | `true` or `false`                                                             | `false`                       | No       |                                                                                                       |
| `context`               | "signin"<br/> "signup"<br/> "use"                                             | "signin"                      | No       |                                                                                                       |
| `cancel_on_tap_outside` | `true` or `false`                                                             | `true`                        | No       |                                                                                                       |
| `prompt_position`       | "left"<br/> "center"<br/> "right"                                             | "left"                        | No       |                                                                                                       |

## Data Type: AccountInfo

This data type contains following values.
| Property | Description |
|----------|---------|
| `fullName` | User's full name |
| `username` | User's email or phone number |
| `photoUrl` | base64-encoded dataURI representing the user's avatar. If the user has set no avatar, its value will be `null`|
| `id` | a GUID that is unique across all Microsoft accounts |

We recommend using the `id` as a key, rather than the email address, because an email address isn't a unique account identifier. It's possible for a user to use a Gmail address for a Microsoft Account, and to potentially create two different accounts (a Microsoft account and a Google account) with that same email address. It's also possible for a Microsoft Account user to change the primary email address on their account.

## Data Type: SignInAccountInfo

This data type contains all the fields of [AccountInfo](#data-type-accountinfo) and a new field `idToken`.
| Property | Description |
|----------|---------|
| `fullName` | User's full name |
| `username` | User's email or phone number |
| `photoUrl` | base64-encoded dataURI representing the user's avatar. If the user has set no avatar, its value will be `null`|
| `id` | a GUID that is unique across all Microsoft accounts |
| `idToken` | [ID token](https://docs.microsoft.com/en-us/azure/active-directory/develop/id-tokens) received during sign-in process |

We recommend using the `id` as a key, rather than the email address, because an email address isn't a unique account identifier. It's possible for a user to use a Gmail address for a Microsoft Account, and to potentially create two different accounts (a Microsoft account and a Google account) with that same email address. It's also possible for a Microsoft Account user to change the primary email address on their account.

## Method: ms.auth.initialize

`ms.auth.initialize` is called to initialize Microsoft Quick Authentication library. It takes [InitConfiguration](#data-type-initconfiguration) object as argument. The following code example shows usage in `onload` function:

```javascript
window.onload = function () {
  const result = ms.auth.initialize({
    client_id: '<your application client ID>',
    callback: handleSignInResponse,
    login_uri: '<your application redirect URI>',
    cancel_on_tap_outside: false
  });
  if (result.result == 'success') {
    // Proceed.
  } else {
    // Initialization failed.
    console.error('ms.auth.initialize failed: ', result);
  }
};
```

1. Set `client_id` to the Application Client ID you received from Azure.
1. Set `callback` to the name of the JavaScript function you'd like called when a user is authenticated.
1. Set `login_uri` to the redirect URI specified in your application registration in Azure portal. If this property isn't set, then for website https://abc.com, Quick Authentication library will use https://abc.com/blank.html as the default.

If `ms.auth.initialize` succeeds, it will return `{result: 'success'}`. If it fails, it will return `{result: 'failure', reason: <string-explaining-why-it-failed>}`.

The following are some possible reasons for failure:

- Initialization was called more than once. Here API returns `{result: 'failure', reason: 'Library already initialized'}`.
- `callback` isn't a valid function or `client_id` isn't set. In these cases, API returns `{result: 'failure', reason: 'Invalid configuration'}`.

`ms.auth.initialize` or div ["ms-auth-initialize"](quick-authentication-how-to.md#option-1-add-sign-in-button-via-html) is needed to initialize Microsoft Quick Authentication library.

If initialization isn't done, all other API calls will fail.

## Data Type: ButtonConfiguration

This configuration object needs to be passed as argument to [ms.auth.renderSignInButton](#method-msauthrendersigninbutton) method.

| Property                          | Values                                                              | Default       | Required |
|-----------------------------------|---------------------------------------------------------------------|---------------|----------|
| [type](#type)                     | "standard"<br/> "icon"                                              | "standard"    | No       |
| [theme](#theme)                   | "dark"<br/> "light"                                                 | "dark"        | No       |
| [size](#size)                     | "small"<br/> "medium"<br/> "large"                                  | "large"       | No       |
| [text](#text)                     | "signin_with"<br/> "signup_with"<br/> "continue_with"<br/> "signin" | "signin_with" | No       |
| [shape](#shape)                   | "rectangular"<br/> "rounded"<br/> "pill"                            | "rectangular" | No       |
| `width`                           | number in CSS pixels<br/> 200–600                                   |               | No       |
| `height`                          | number in CSS pixels<br/> 24–100                                    |               | No       |
| [logo_alignment](#logo_alignment) | "left"<br/> "center"                                                | "left"        | No       |

## Method: ms.auth.renderSignInButton

`ms.auth.renderSignInButton` is called to render a sign-in button. See the following code example for understanding usage of this method:

```html
<div id="ms-button-holder"></div>
<script>
function addMicrosoftSignInButton() {
  const parent = document.getElementById('ms-button-holder');
  const options = {theme: 'light'}; // use light theme.
  ms.auth.renderSignInButton(parent, options);
};
</script>
```

It takes the following arguments:

1. `parent`: The HTMLElement under which this button will be rendered.
1. `options`: An object of type [ButtonConfiguration](#data-type-buttonconfiguration).

If `ms.auth.renderSignInButton` is called before initialization has been done or if parent (first argument) isn't set, then it will throw a string explaining the problem.

If the second argument (`options`) isn't set, then it uses default values mentioned in [button configuration table](#data-type-buttonconfiguration).

## Method: ms.auth.signOut

`ms.auth.signOut` is used to sign out a user. See the following code example for understanding usage of this method:

```javascript
ms.auth.signOut(username, function (result) {
  if (result.result) {
    // Finish the logout process in your website.
  } else {
    console.log('Sign out failed, error: ', result.error);
  }
});
```

You'll need to pass in `username` field of [AccountInfo](#data-type-accountinfo) object you received as part of the authentication event and a callback to receive the result of the `signOut()` call. The argument returned to the callback will be an object with the following structure:

- `result` - `true` if the user was signed out, `false` if not
- `error` - if `result==false`, will be an object with a `message` property explaining the error

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

If the `callback` isn't a valid function, then also this API will throw exception.
If `username` isn't found, the `callback` will be called with `{result: 'failure', error: 'username not found'}`.

## Method: ms.auth.startSignIn

`ms.auth.startSignIn` can be used to begin sign-in process programmatically. See the following code example for understanding usage of this method:

```javascript
button.addEventListener('click', function() {
  ms.auth.startSignIn();
});
```

Successful authentications will be routed into the [callback](#callback) defined when initializing the library.

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

## Method: ms.auth.startGetCurrentAccount

`ms.auth.startGetCurrentAccount` can be used to determine if the current user signed-in. See the following code example for understanding usage of this method:

```javascript
function accountCallback(account_info) {
  if (account_info) {
    // Use account.
  }
}

ms.auth.startGetCurrentAccount(accountCallback);
```

It takes as argument a function. On completion, this function will be called with [AccountInfo](#data-type-accountinfo) representing the signed-in user.

If the user is signed-in, [AccountInfo](#data-type-accountinfo) will be a valid object. If the user isn't signed-in, the argument will be `null`.

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

## Data Type: PromptMomentNotification

`PromptMomentNotification` has the following structure:

- `type` - the moment type as a `String`; will be one of
  - "display" - Occurs after `prompt()` method is called. If prompt shows, `displayed` property will be true, else `displayed` will be false.
  - "skipped" - Occurs when the prompt is closed by user manually canceling the prompt or closing prompt by tapping outside, etc.
  - "dismissed" - Occurs when a) credentials were successfully retrieved b) `ms.auth.cancel` was called to close the prompt.
- `displayed`    - A boolean based on whether the UI is displayed; will be `undefined` if `type` isn't "display"
- `reason` - the reason the notification callback was called as a `String`; will be `undefined` if `type` is "display" and `displayed` is `true`.

 The value of `reason` will vary based on the `type` value:

- `type == "display"`
  - "another_prompt_running"
  - "browser_not_supported"
  - "in_cooldown_period"
  - "non_msa_profile"
  - "unknown"
- `type == "skipped"`
  - "tap_outside"
  - "user_cancelled"
  - "unknown"
- `type == "dismissed"`
  - "cancel_called"
  - "credential_returned"

## Method: ms.auth.prompt

`ms.auth.prompt()` method can be used to control the display of enhanced sign-in prompt in MSA profile in Microsoft Edge. See the following code example for understanding usage of this method:

```javascript
ms.auth.prompt('right', function(notification) {
  const reason = notification.reason;
  if (notification.type === 'display' && !notification.displayed) {
    if ( reason === 'browser_not_supported' ) {
      console.log('prompt not supported in browser');
    }
  } else if (notification.type === 'skipped') {
    if (reason === 'user_cancel') {
      console.log('user cancelled');
    }
  } else if (notification.type === 'dismissed') {
    if (reason === 'credential_returned') {
      console.log('Got sign-in credentials');
    }
  }
});
```

This method may be called with no arguments to use the default configuration. You may also supply the following arguments to customize its appearance and/or respond to specific user interactions with the prompt.

The first argument is the position. By default, the prompt is rendered on the left. You can position it "center" or "right" as well.

The second argument is a callback function that receives notifications from the prompt, based on user interactions. The callback receives a [PromptMomentNotification](#data-type-promptmomentnotification) object when the user interacts with it.

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

If the `callback` is specified in second argument isn't `null` or `undefined`, it has to be a valid function, otherwise this API will throw exception.

The sign-in prompt will only show in a profile signed in with MSA account in Microsoft Edge. For non-MSA profile in Microsoft Edge, it will not be displayed and [PromptMomentNotification](#data-type-promptmomentnotification) will have `reason === 'non_msa_profile'`. For other browsers, [PromptMomentNotification](#data-type-promptmomentnotification) will have `reason === 'browser_not_supported'`.

## Method: ms.auth.cancel

`ms.auth.cancel` can be used to close the enhanced sign-in prompt in MSA profile in Microsoft Edge. See the following code example for understanding usage of this method:

```javascript
ms.auth.cancel();
```

This method will be a no-op if there's no prompt showing.

If a prompt was showing and it was dismissed using this method, then the callback registered with [ms.auth.prompt](#method-msauthprompt) will receive [PromptMomentNotification](#data-type-promptmomentnotification) object `{ type: "dismissed", reason: "cancel_called" }`.

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

## Method: ms.auth.getMSALAccount

Quick Authentication uses [MSAL.js](https://github.com/AzureAD/microsoft-authentication-library-for-js/tree/dev/lib/msal-browser) internally.
MSAL.js provides functionality for fetching tokens. Quick Authentication exposes APIs to use MSAL.js functionality for fetching token.

`ms.auth.getMSALAccount` method can be used to get MSAL account info, which is needed to fetch MSAL token. See the following code example for understanding usage of this method:

```javascript
const msalAccount = ms.auth.getMSALAccount(accountInfo.username);
if (msalAccount) {
  // Use the MSAL account.
} else {
  console.log(`No MSAL account exists for ${accountInfo.username}`);
}
```

`username` is the username field in [AccountInfo](#data-type-accountinfo), which was returned to the callback after a successful sign-in.

If it succeeds, the API will return the [MSAL account information](https://azuread.github.io/microsoft-authentication-library-for-js/ref/modules/_azure_msal_common.html#accountinfo) corresponding to the username.

If the account can't be found, `null` will be returned.

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

## Method: ms.auth.acquireTokenSilent

`ms.auth.acquireTokenSilent` can be used to fetch tokens silently. See the following code example for understanding usage of this method:

```javascript
function tokenFetchResponse(response) {
  if (response && response.accessToken) {
    // Use accessToken.
  }
}

const request = {
  scopes: ["User.Read"],
  account: ms.auth.getMSALAccount(accountInfo.username),
}
if (!request.account) {
  console.log('Silent token fetch failed: Account not found');
} else {
  ms.auth.acquireTokenSilent(request).then(tokenFetchResponse).catch(err => {
    console.log("Token fetch failed with error: " , err);
  });
}
```

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

Check [MSAL.js access token fetch documentation](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/acquire-token.md) for more information. Also check [MSAL.js acquireTokenSilent](https://azuread.github.io/microsoft-authentication-library-for-js/ref/classes/_azure_msal_browser.publicclientapplication.html#acquiretokensilent) API documentation.

## Data Type: ms.auth.InteractionRequiredAuthError

`ms.auth.InteractionRequiredAuthError` is error type thrown in case [ms.auth.acquireTokenSilent](#method-msauthacquiretokensilent) fails with user interaction. In such a case, [ms.auth.acquireTokenPopup](#method-msauthacquiretokenpopup) can be used to fetch the token.

## Method: ms.auth.acquireTokenPopup

`ms.auth.acquireTokenPopup` can be called to fetch tokens in case fetching tokens silently fail. See the following code example for understanding usage of this method:

```javascript
function tokenFetchResponse(response) {
  if (response && response.accessToken) {
    // Use accessToken.
  }
}

const request = {
  scopes: ["Mail.Read"],
  account: ms.auth.getMSALAccount(accountInfo.username),
}
if (request.account) {
  ms.auth.acquireTokenSilent(request).then(tokenFetchResponse).catch(err => {
    if (err instanceof ms.auth.InteractionRequiredAuthError) {
      ms.auth.acquireTokenPopup(request);
    }
  });
}
```

If this method is called before initialization has been done using [ms.auth.initialize](#method-msauthinitialize) or using div ["ms-auth-initialize"](./quick-authentication-how-to.md#option-1-add-sign-in-button-via-html), then it will throw exception.

Check [MSAL.js access token fetch documentation](https://github.com/AzureAD/microsoft-authentication-library-for-js/blob/dev/lib/msal-browser/docs/acquire-token.md) for more information. Also check [MSAL.js acquireTokenPopup](https://azuread.github.io/microsoft-authentication-library-for-js/ref/classes/_azure_msal_browser.publicclientapplication.html#acquiretokenpopup) API documentation.
