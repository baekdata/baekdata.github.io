---
layout: post
title: goooood 활용  활용 및 예제
tags:
  - android
  - ui
  
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

####만나서 반갑습니다.

```java
    /**
     * 상품팝업 타입 인지 여부
     */
    private boolean mIsPopupType;``
    private int mPopupTopPadding = 0;

    public SellerHomeProductAdapter(Context context, boolean isPopupType) {
        mContext = context;
        mIsPopupType = isPopupType;
        ArrayList<ObjectItem> data = new ArrayList<>();
        mCommonProductRecyclerAdapterHelper = new CommonProductRecyclerAdapterHelper(context, data);
        if(mIsPopupType){
            mPopupTopPadding = DisplayUtil.dpToPx(mContext, 10);
        }

    }
```


The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.