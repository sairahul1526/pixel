---
layout:     post
title:      Image Slideshow using ViewPager with PagerAdapter
date:       2016-10-11 12:31:19
summary:    Perhaps you’ve seen some of the new user interface features available as part of the Android compatibility package. One such feature, horizontal view paging, allows for easy left and right swipes to load different screens (pages), controlled by a single Activity. This feature has been showcased in several high profile applications like the Android Market application and the Google+ Android client.
categories: jekyll pixyll
author:     BHARDADWAJ SHARMA
permalink:  /image-slideshow-using-viewpager-with-pageadapter/
tags:
  - android
---

{% highlight xml %}
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:id="@+id/relativeLayout">


    <android.support.v4.view.ViewPager xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/pager"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    </android.support.v4.view.ViewPager>

</RelativeLayout>
{% endhighlight %}

{% highlight java %}
CustomAdapter mCustomPagerAdapter = new CustomPagerAdapter(this);
 
ViePager mViewPager = (ViewPager) findViewById(R.id.pager);
mViewPager.setAdapter(mCustomPagerAdapter);
{% endhighlight %}

{% highlight java %}
int[] mResources = {
        R.drawable.first,
        R.drawable.second,
        R.drawable.third,
        R.drawable.fourth,
        R.drawable.fifth,
        R.drawable.sixth
};
{% endhighlight %}

{% highlight java %}
class CustomPagerAdapter extends PagerAdapter {
 
    Context mContext;
    LayoutInflater mLayoutInflater;

    int[] mResources = {
        R.drawable.first,
        R.drawable.second,
        R.drawable.third,
        R.drawable.fourth,
        R.drawable.fifth,
        R.drawable.sixth
	};
 
    public CustomPagerAdapter(Context context) {
        mContext = context;
        mLayoutInflater = (LayoutInflater) mContext.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
    }
 
    @Override
    public int getCount() {
        return mResources.length;
    }
 
    @Override
    public boolean isViewFromObject(View view, Object object) {
        return view == ((LinearLayout) object);
    }
 
    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        View itemView = mLayoutInflater.inflate(R.layout.pager_item, container, false);
 
        ImageView imageView = (ImageView) itemView.findViewById(R.id.imageView);
        imageView.setImageResource(mResources[position]);
 
        container.addView(itemView);
 
        return itemView;
    }
 
    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        container.removeView((LinearLayout) object);
    }
}
{% endhighlight %}

{% highlight xml %}
<?xml version="1.0" encoding="utf-8"?>
 
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
 
    <ImageView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/imageView" />
</LinearLayout>
{% endhighlight %}

---
