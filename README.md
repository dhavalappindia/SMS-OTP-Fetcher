# SMS-OTP-Fetcher
Get OTP From SMS and set in edittext

A library for implementing interception of SMS with a verification code using a few lines of code.

Who we are
Need iOS and Android apps, MVP development or prototyping? . We develop software since 2009, and we're known experts in this field.


Usage

Add permissions to AndroidManifest.xml:

  <uses-permission android:name="android.permission.RECEIVE_SMS" />
  <uses-permission android:name="android.permission.READ_SMS" />
Init SmsVerifyCatcher in method like onCreate activity:

    smsVerifyCatcher = new SmsVerifyCatcher(this, new OnSmsCatchListener<String>() {
        @Override
        public void onSmsCatch(String message) {
            String code = parseCode(message);//Parse verification code
            etCode.setText(code);//set code in edit text
            //then you can send verification code to server
        }
    });
Override activity lifecicle methods:

    @Override
    protected void onStart() {
        super.onStart();
        smsVerifyCatcher.onStart();
    }

    @Override
    protected void onStop() {
        super.onStop();
        smsVerifyCatcher.onStop();
    }

    /**
     * need for Android 6 real time permissions
     */
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        smsVerifyCatcher.onRequestPermissionsResult(requestCode, permissions, grantResults);
    }
You can set phone number filter:

    smsVerifyCatcher.setPhoneNumberFilter("777");
or set message filter via regexp:

   smsVerifyCatcher.setFilter("<regexp>");
That's all! Take a look at the sample project for more information





