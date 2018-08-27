---
layout: post
title: "Goole Voice사용 시 focus잃었을 시 해결 방안"
tags: [Android,  Google]
comments: true
---

> RecognizerIntent.ACTION_RECOGNIZE_SPEECH를 활용한 GooleVoice  

---



* EditText에 뷰 근처나 혹은 키보드 쪽에서 GoogleVoice 활용 

```java
 Intent intent = new Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH);
            intent.putExtra(RecognizerIntent.EXTRA_PROMPT, getString(R.string.voice_search_title));
            intent.putExtra(RecognizerIntent.EXTRA_LANGUAGE_MODEL, RecognizerIntent.LANGUAGE_MODEL_FREE_FORM);
            intent.putExtra(RecognizerIntent.EXTRA_MAX_RESULTS, REQUEST_VOICE_SEARCH);
            intent.putExtra(RecognizerIntent.EXTRA_LANGUAGE, "ko-KR");
            startActivityForResult(intent, REQUEST_VOICE_SEARCH);
```

> 음성을 제대로 넘겼을 경우는 괜찮지만, 넘기지 못했거나 실행하지 못했을 경우 focus를 잃는다
> 이럴 경우, EditTextView focus를 가기 위해서는 임의로 가야하기 때문에 불편하다.

---
**따라서 해결방법으로는 음성 dialog가 종료될 경우 onResume()이 불리므로 onResume()에서 requestFocus를 
호출해주면 해결이 가능해진다. ex)editTextView.requestFocus(true);**

* 그러나 이럴 경우, 안되는 것을 확인할 수 있다.
 * 바로 하게 될 경우, 그리는 시점과 맞물려서 제대로 처리가 되지 않는다.
 * 따라서 handler를 활용하여 적당히 delay를 주어 처리해야 확인이 가능하다.

```java
       mHandler.postDelayed(mInputMessageFocusRunnable, 200);
    }

    private Runnable mInputMessageFocusRunnable = new Runnable() {
        @Override
        public void run() {
            mInputMessage.requestFocus();
        }
    };
```

> 주의할 점은 delay가 아니라 post(new Runnable){}만을 줄 경우 focus가 갈 때 키보드창까지 오픈이 되어버리는 것을 확인할 수 있다. 따라서 위처럼 Delay를 일정시간 주어야 한다.  


    

---
[google developers guide - google voice input 링크 ](https://developers.google.com/glass/develop/gdk/voice)

