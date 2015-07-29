title: "ActionBarCompat"
date: 2015-03-11 17:34:39
tags:
---

1. 有三种Theme：
    Theme.AppCompat 深色主题，继承自android:Theme
    Theme.AppCompat.Light 浅色主题，继承自android:Theme.Light
    Theme.AppCompat.Light.DarkActionBar 浅色主题，ActionBar是深色主题，继承自android:Theme.Light

2. 可以使用ActionBarStyleGenerator开始进行自定义，不过功能有限，只能自定义背景色，图标和前景色通常还需要自行修改。另外这个站点生成的文件命名采用添加后缀的方式，不是很符合android的风格。

3. 所有属性进行自定义时，需要同时添加android:xxx和xxx两项，前者v14+使用，后者v14-使用或者使用values和values-v14分别定义

4. ActionBar默认大小
    以Galaxy Nexus portrait模式为例
    高度：48dp(portrait), 40dp(landcape)
    右侧按钮宽度：56dp
    paddingLeft、paddingRight：12dp

5. 自定义方式：修改Theme里的属性，或者actionBarWidgetTheme里面的属性
     如果属性是color/dimen/drawable，则可以直接设置
     如果属性是textAppearance/style，则还需要进一步定义，此时要注意该属性值需要继承自合适的类型
     某些dimen属性无法修改，可以通过修改图标大小的方式间接完成，例如想让up图标距离两侧的边距增大，就只能够修改up图标大小，让两侧的透明区域增大

6. ActionBar的自定义包括：

		ActionBar的自定义：背景、标题、进度条、按钮
		
		actionBarStyle: << Widget.AppCompat.Light.ActionBar.Solid.Inverse
          background/backgroundStacked/backgroundSplit: Drawable
          titleTextStyle: << TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse
          subtitleTextStyle: << TextAppearance.AppCompat.Widget.ActionBar.Subtitle.Inverse
          progressBarStyle: << Widget.AppCompat.ProgressBar.Horizontal 
          indeterminateProgressStyle: << Widget.AppCompat.ProgressBar
          divider: << Drawable
          displayOptions:useLogo|showHome|homeAsUp|showTitle|showCustom
		
		actionButtonStyle: << Widget.AppCompat.ActionButton
          background: Drawable, 默认为?attr/actionBarItemBackground
          
          
	** abc_action_menu_item_layout为布局文件，paddingLeft/Right为8，paddingTop/Bottom为4，不可修改，因此portrait模式下图标大小应该不超过40dp(56-2\*8) x 40dp(48-2\*4)，而landscape模式下由于action bar高度仅为40dp，因此图标大小不超过32dp x 32dp。所以通常做图标时取小的尺寸做成32dp x 32dp**
	
		actionOverflowButtonStyle: << Widget.AppCompat.ActionButton.Overflow
          src: Drawable
	**使用OverflowMenuButton实现，没有使用布局资源，默认paddingLeft/Right为12，因此Overflow图标的建议大小为32dp(56-12\*2) x 32dp**
	
		homeAsUpIndicator: << Drawable
		actionBarSize: dimen 高度

		ActionMode的自定义：背景，左侧对勾图标
		  actionModeBackground/actionModeSplitBackground: Drawable
		  actionModeCloseButtonStyle: << Widget.AppCompat.ActionButton.CloseMode
		  actionModeCloseDrawable: Drawable

		Spinner的样式: 
		     actionBarWidgetTheme
          		actionDropDownStyle: << Widget.AppCompat.Spinner.DropDown.ActionBar
               		background: Drawable
               		popupBackground: Drawable
               		dropDownSelector: Drawable

		SpinnerItem的样式通过SpinnerAdapter的getView进行设置

		OverflowMenu的样式：实现类MenuPopupHelper
		     actionBarWidgetTheme
		          popupMenuStyle
		               popupBackground: Drawable
		          dropDownListViewStyle
		               listSelector: Drawable
		               divider: Drawable
     
		OverflowMenu Item的样式: 高度、字体 (默认布局：abc_popup_menu_item_layout)
		     actionBarWidgetTheme
		          textAppearanceLargePopupMenu: << TextAppearance.AppCompat.Widget.PopupMenu.Large
		          dropdownListPreferredItemHeight: dimen
     

7. 对ABC代码的修改：在2.x版本的系统上依旧显示Overflow Button：ActionBarPolicy#showsOverflowMenuButton，始终返回true