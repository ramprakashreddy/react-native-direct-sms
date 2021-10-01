# react-native-direct-sms

## Getting started

`$ npm install react-native-direct-sms --save`

### Mostly automatic installation

`$ react-native link react-native-direct-sms`

## Usage
```javascript
import DirectSms from 'react-native-direct-sms';

DirectSms
.sendDirectSms('999...', 'This is a direct sms')
.then(()=>{
    console.log("sms sent");
})
.catch((e)=>{
    console.log("have a error", e);
})
 
```

## User Permission

```javascript
async function sendDirectSms(number, message) {
    try {
        const granted = await PermissionsAndroid.request(
        PermissionsAndroid.PERMISSIONS.SEND_SMS,
            {
                title: 'App Sms Permission',
                message:
                'App needs access to your inbox         ' +
                'so you can send messages in background.',
                buttonNeutral: 'Ask Me Later',
                buttonNegative: 'Cancel',
                buttonPositive: 'OK',
            },
        );
        if (granted === PermissionsAndroid.RESULTS.GRANTED) {
         const messageStatus =  await DirectSms.sendDirectSms(number, message);
        } else {
            console.log('SMS permission denied');
        }
    } catch (err) {
        console.warn(err);
    }
}

```
## Sample Code Snippet


```javascript
import React from 'react';
import {Button, StyleSheet, View,PermissionsAndroid,ToastAndroid} from 'react-native';
import DirectSms from 'react-native-direct-sms';
export default function App() {
  async function SEND_SMS(number, messageText) {
    try {
        const granted = await PermissionsAndroid.request(
        PermissionsAndroid.PERMISSIONS.SEND_SMS,
            {
                title: 'App Sms Permission',
                message:
                'App needs access to your inbox' +
                'so you can send messages in background.',
                buttonNeutral: 'Ask Me Later',
                buttonNegative: 'Cancel',
                buttonPositive: 'OK',
            },
        );
        console.log(granted)
        if (granted === PermissionsAndroid.RESULTS.GRANTED) {
         const messageStatus =  await DirectSms.sendDirectSms(number, messageText);
         console.log(messageStatus)
         ToastAndroid.show('SMS Sent Successfully',ToastAndroid.SHORT);
        } else {
            ToastAndroid.show('SMS permissions are denied',ToastAndroid.SHORT);
        }
    } catch (err) {
        console.warn(err);
    }
  }
  return (
   <View style={{flex:1,justifyContent:"center"}}>
    <View style={{width:200,alignSelf:"center"}}>
    <Button
     title="SEND SMS"
     onPress={()=>{
      SEND_SMS("1234567890","HELLO! This is a test message")
      //Replace 1234567890 with req. phone number
     }}
     />
    </View>
   </View>
  );
}
```
