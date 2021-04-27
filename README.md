# capacitor-plugin-app-tracking-transparency

Capacitor plugin to request user authorization to access app-related data for tracking the user or the device. iOS only.

Read more about Apple's App Tracking Transparency framework [here](https://developer.apple.com/documentation/apptrackingtransparency). Also [this](https://developer.apple.com/app-store/user-privacy-and-data-use/) might be a good read.

## Platform support

iOS only but with web fallback for development purposes.

## Maintainers

| Maintainer | GitHub                                    | Social                                        |
| ---------- | ----------------------------------------- | --------------------------------------------- |
| Manuel Heidrich | [mahnuh](https://github.com/mahnuh) | [@mahnuh](https://twitter.com/mahnuh) |
| prototype.berlin GmbH | [prototype-berlin](https://github.com/prototype-berlin) | [@prototypeberlin](https://twitter.com/prototypeberlin) |

## Installation

```
npm install capacitor-plugin-app-tracking-transparency
npx cap sync
```

## Configuration

Add this to your app's Info.plist and update the message according to your needs:

```xml
<key>NSUserTrackingUsageDescription</key>
<string>Your data will be used to deliver personalized apps to you.</string>
```


## Usage

```typescript
import { Plugins } from '@capacitor/core';
import 'capacitor-plugin-app-tracking-transparency'; // only if you want web support

// Type Safe. Current capacitor 2 limitation
import {
  AppTrackingTransparencyPlugin,
  AppTrackingStatusResponse,
} from 'capacitor-plugin-app-tracking-transparency';

const AppTrackingTransparency = Plugins.AppTrackingTransparency as AppTrackingTransparencyPlugin;


public async getStatus(): Promise<AppTrackingStatusResponse> {
  const response = await AppTrackingTransparency.getStatus();

  console.log(response);
  // { status: 'authorized' } for example

  return response;
}

public async requestPermission(): Promise<AppTrackingStatusResponse> {
  const response = await AppTrackingTransparency.requestPermission();

  console.log(response);
  // { status: 'authorized' } for example

  return response;
}
```

Both available methods return `AppTrackingStatusResponse` with `status: AppTrackingStatus`, which will be one of the following: `authorized`, `denied`, `notDetermined` or `restricted`. See [Apple's docs](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus) for reference.

## License

See [LICENSE](https://github.com/mahnuh/capacitor-plugin-app-tracking-transparency/blob/main/LICENSE).