# Change Log
### 1.2.5 (September 2, 2020)
* Enhanced prerequisite check in `init()`.
* Improved stability.
### 1.2.4 (August 19, 2020)
* Bug fix
    * Fixed the connection problem with Android SDK.
### 1.2.3 (August 13, 2020)
* Bug fix
    * Fixed the unexpected exceptions.
* Improved stability
### 1.2.2 (July 28, 2020)
* Replaced MediaDeviceInfo with InputDeviceInfo in following `SendBirdCall` methods
    * `getCurrentAudioInputDevice(): InputDeviceInfo`
    * `getAvailableAudioInputDevices(): InputDeviceInfo[]`
    * `selectAudioInputDevice(mediaDeviceInfo: InputDeviceInfo): void`
    * `getCurrentVideoInputDevice(): InputDeviceInfo`
    * `getAvailableVideoInputDevices(): InputDeviceInfo[]`
    * `selectVideoInputDevice(mediaDeviceInfo: InputDeviceInfo): void`
* Added missing type information
    * `SendbirdCall`'s `useMedia()` method can return `undefined`
    * `DirectCall`'s `setLocalMediaView(mediaView: HTMLMediaElement)`
    * `DirectCall`'s `setRemoteMediaView(mediaView: HTMLMediaElement)`
* Added webhook support
    * Add `handleWebhookData(data: WebhookData): void` to SendBirdCall
    * Add `WebhookData` interface

### 1.2.1 (July 21, 2020)
* Buf fix
    * Fixed the unexpected exceptions in safari.
### 1.2.0 (July 20, 2020)
* Added support for Peer-to-peer call.
    * The Peer-to-peer option can be configured on the dashboard.
* Added getting ongoing call count and ongoing status of `DirectCall`.
    * Added `getOngoingCallCount(): number` to `SendBirdCall`.
    * Added `readonly isOngoing: boolean` to `DirectCall`.
* Added `setCallConnectionTimeout(timeout: number): void` to `SendBirdCall`.
    * The call connection timer starts when the callee accepts the call. The timer will end the call after the specified timeout interval.
* Improved stability.
### 1.1.4 (July 14, 2020)
* Bug fix
    * Fixed typo in `d.ts`.
    * Fixed import error in Node environment.
### 1.1.3 (June 18, 2020)
* Improved stability.
### 1.1.2 (June 16, 2020)
* Improved stability.
### 1.1.1 (May 25, 2020)
* Bug fix
    * Fixed the bug that some console logging ignored `LoggerLevel`.
### 1.1.0 (May 22, 2020)
* Below property is added in `SendBirdCall`
    * `ErrorCode`
* Below keys are added in `SendBirdCall.LoggerLevel`
    * `WARNING`
    * `INFO`
* Below property is added in `DirectCall`
    * `readonly callLog`
* Below property is added in `DirectCallLog`
    * `readonly isFromServer`
### 1.0.2 (May 1, 2020)
* Below methods are added in `SendBirdCall`
    * `setRingingTimeout(timeout: int): void`
* Optimized video call frame rate.
* Improved stability.
### 1.0.1 (Mar 25, 2020)
* Bug fix
    * Fixed the bug that `onRemoteVideoSettingsChanged` doesn't fire.
* The default value of `callOption.videoEnabled` is changed to `ture`.
### 1.0.0 (Mar 24, 2020)
* README has been updated. Refer to readme to learn how to configure media devices. 
* Interfaces for media devices are added / changed.
    * Below methods are added in `SendBirdCall`
        * `getCurrentVideoInputDevice(): MediaDeviceInfo`
        * `getAvailableVideoInputDevices(): MediaDeviceInfo[]`
        * `selectVideoInputDevice(mediaDeviceInfo: MediaDeviceInfo): void`
        * `updateMediaDevices(constraints: { audio: boolean; video: boolean }): void`
        * `useMedia(constraints: { audio: boolean; video: boolean }): MediaAccess`
    * Below event listener is added in `SendBirdCallListener`
        * `onVideoInputDeviceChanged: ((currentVideoInputDevice: MediaDeviceInfo, availableVideoInputDevices: MediaDeviceInfo[]) => void) | null`
    * Below methods are changed in `SendBirdCall`
        * `getCurrentVideoInputDevice(): MediaDeviceInfo`
        * `getAvailableAudioInputDevices()` is now synchronous
        * `selectAudioInputDevice(mediaDeviceInfo: MediaDeviceInfo)` is now synchronous
        * `getAvailableAudioOutputDevices()` is now synchronous
        * `selectAudioOutputDevice(mediaDeviceInfo: MediaDeviceInfo)` is now synchronous

* Deprecated methods are removed
    * In `SendBirdCall`,
        * `dial(userId: string, isVideoCall: boolean, callOption: DirectCallOption, callback?: DialHandler): DirectCall` is removed. Use `dial(params: DialParams, callback?: DialHandler): DirectCall` instead.
    * In `DirectCall`,
        * `onRemoteAudioEnabled` event listener is removed. Use `onRemoteAudioSettingsChanged` instead.
        * `accept(callOption: DirectCallOption)` is removed. Use `accept(params: AcceptParams): void` instead.
        * `mute()` is removed. Use `muteMicrophone()` instead.
        * `unmute()` is removed. Use `unmuteMicrophone()` instead.
    * In `DirectCallOption`
        * `localVideoView` is removed. Use `localMediaView` instead.
        * `remoteVideoView` is removed. Use `remoteMediaView` instead.

### 0.9.0 (Mar 18, 2020)
* Internal improvement
### 0.8.1 (Mar 13, 2020)
* Bug fix
    * Fixed error when user accepted call without specifying localMediaView
* Below properties are added in `DirectCall`
    * `readonly callId: string`
    * `readonly isEnded: boolean`

### 0.8.0 (Mar 9, 2020)
* Interface for video call has been implemented
    * Below properties are added in `DirectCall`
        * `readonly isLocalVideoEnabled: boolean`
        * `readonly isRemoteVideoEnabled: boolean`
        * `readonly localMediaView: HTMLMediaElement`
        * `readonly remoteMediaView: HTMLMediaElement`

    * Below methods are added in `DirectCall`
        * `setLocalMediaView(): Promise<void>`
        * `setRemoteMediaView(): Promise<void>`
        * `stopVideo(): void`
        * `startVideo(): void`

    * Below implementable event listeners are added in `DirectCall`
        * `onRemoteVideoSettingsChanged: ((call: DirectCall) => void) | null`

    * Below property is added in `DirectCallOption`
        * `videoEnabled?: boolean`

* Wrong type definitions have been fixed
    * Type definitions for below methods in class `SendBirdCall` has been fixed.
        * `getAvailableAudioInputDevices(): MediaDeviceInfo[]` -> `getAvailableAudioInputDevices(): Promise<MediaDeviceInfo[]>`
        * `selectAudioInputDevice(mediaDeviceInfo: MediaDeviceInfo): void` -> `selectAudioInputDevice(mediaDeviceInfo: MediaDeviceInfo): Promise<void>`
        * `getAvailableAudioOutputDevices(): MediaDeviceInfo[]` -> `getAvailableAudioOutputDevices(): Promise<MediaDeviceInfo[]>`
        * `selectAudioOutputDevice(mediaDeviceInfo: MediaDeviceInfo): void` -> `selectAudioOutputDevice(mediaDeviceInfo: MediaDeviceInfo): Promise<void>`

### 0.7.0 (Feb 21, 2020)
* Selecting an audio input / output device is implemented.
    * Below methods are added in `SendBirdCall`
        * `getCurrentAudioInputDevice(): MediaDeviceInfo`
        * `getAvailableAudioInputDevices(): MediaDeviceInfo[]`
        * `selectAudioInputDevice(mediaDeviceInfo: MediaDeviceInfo): void`
        * `getCurrentAudioOutputDevice(): MediaDeviceInfo`
        * `getAvailableAudioOutputDevices(): MediaDeviceInfo[]`
        * `selectAudioOutputDevice(mediaDeviceInfo: MediaDeviceInfo): void`
    * Below implementable event listeners are added in `SendBirdCallListener`
        * `onAudioInputDeviceChanged: ((currentAudioInputDevice: MediaDeviceInfo, availableAudioInputDevices: MediaDeviceInfo[]) => void)  | null`
        * `onAudioOutputDeviceChanged: ((currentAudioOutputDevice: MediaDeviceInfo, availableAudioOutputDevices: MediaDeviceInfo[]) => void)  | null`


* Setting / retrieving custom items is implemented.
    * Below methods are added in `SendBirdCall`
        * `updateCustomItems(callId: string, customItems: CustomItems, callback?: CustomItemsHandler): Promise<CustomItemsResult>`
        * `deleteCustomItems(callId: string, customItemKeys: string[], callback?: CustomItemsHandler): Promise<CustomItemsResult>`
        * `deleteAllCustomItems(callId: string, callback?: CustomItemsHandler): Promise<CustomItemsResult>`
    * Below property is added in `DirectCall`
        * `readonly customItems: CustomItems`
    * Below methods are added in `DirectCall`
        * `updateCustomItems(customItems: CustomItems, callback?: CustomItemsHandler): Promise<CustomItemsResult>`
        * `deleteCustomItems(customItemsKeys: string[], callback?: CustomItemsHandler): Promise<CustomItemsResult>`
        * `deleteAllCustomItems(callback?: CustomItemsHandler): Promise<CustomItemsResult>`
    * Below implementable event listeners are added in `DirectCall`
        * `onCustomItemsUpdated: ((call: DirectCall, updatedKeys: string[]) => void) | null`
        * `onCustomItemsDeleted: ((call: DirectCall, deletedKeys: string[]) => void) | null`
    * Below property is added in `DirectCallLog`
        * `readonly customItems: CustomItems`

* Reconnection is implemented in `DirectCall`
    * Below implementable event listeners are added in `DirectCall`
        * `onReconnected: ((call: DirectCall) => void) | null`
        * `onReconnecting: ((call: DirectCall) => void) | null`


* Signature of the `SendBirdCall.dial()` has been changed.
    * `dial(userId: string, isVideoCall: boolean, callOption: DirectCallOption, callback?: DialHandler): DirectCall` is now deprecated
    * `dial(params: DialParams, callback?: DialHandler): DirectCall` is now recommended.

* Signature of the `DirectCall.accept()` has been changed.
    * `accept(callOption: DirectCallOption): void` is now deprecated
    * `accept(params: AcceptParams): void` is now recommended.


### 0.6.10 (Jan 31, 2020)
* Added Typescript Definition.
* Polished error description.
* Properties / Method deprecated. Deprecated interfaces might be removed in future releases.
    * `DirectCall.onRemoteAudioEnabled` is deprecated. Use `onRemoteAudioSettingsChanged` Instead.
    * `DirectCall.mute` is deprecated. Use `muteMicrophone` Instead.
    * `DirectCall.unmute` is deprecated. Use `unmuteMicrophone` Instead.
* Min / max of the `limit` field for `SendBirdCall.createDirectCallLogListQuery` parameter has been adjusted to 10 / 100 each.
* `DirectCall.onRemoteAudioSettingsChanged / onRemoteAudioEnabled` is not fired anymore when actual setting is not changed.


### 0.6.6 (Jan 22, 2020)
* Call is automatically disconnected after certain time (currently 1 min) when one peer leaves call session without explicitly hanging up.
* Removed redundant deprecation warning in `callOption`.


### 0.6.5 (Jan 8, 2020)
* Changed some parameters names of `callOption`.
    * `callOption.localVideoView` and `callOption.remoteVideoView` is now deprecated.
    * `localVideoView` -> `localMediaView`
    * `remoteVideoView` -> `remoteMediaView`

### 0.6.4 (Jan 2, 2020)
* Fixed call.getDuration()

### 0.6.3 (Dec 26, 2019)
* Fixed connection for FireFox, exported LoggerLevel enum

### 0.6.2 (Dec 20, 2019)
* Fixed logger, polyfill

### 0.6.1 (Dec 20, 2019)
* Removed core-js dependency
