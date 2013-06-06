cocos2d-jsb
===========

cocos2d-jsb
```
1\数组的末尾 ，sesquence里面末尾 能够不用null就不用吧。

2\  var animation =cc.Animation.create(null,0.2); 

类似于这种播放动画的 代码，不这样写了。写成如下格式：

var animation =cc.Animation.create(); 

animation.setDelayPerUnit(0.2);

3\跳转代码：能够这样写就这样写最好：

var scene =cc.Scene.create();

scene.addChild(FavorMenu.create());

cc.Director.getInstance().replaceScene(cc.TransitionFade.create(1.2,scene));


那么对应的 场景里面的 函数就要写成

FavorMenu.create = function () {
     var sg = new FavorMenu();
     if (sg && sg.init()) {
         return sg;
     }
     return null;
};

FavorMenu.scene = function () {
     var scene = cc.Scene.create();
     var layer = FavorMenu.create();
     scene.addChild(layer);
     return scene;
};

好像是 cocos2d老版本的写法，新版本跳转和场景对应上了应该也过的去


4\tag只能用整形数

5\cc.CallFunc.create(this.onCallback1, this)，方法在前 this在后。  

6\ 如果可以的话，请把cc.Rect.CCRectContainsPoint写成cc.rectContainsPoint

7\能够不用touch就不用，多用imageItem

8\cc.PointZero 写成 cc.p(0,0)

9\类似于ball11.getBoundingBox().size.height直接写成ball11.getContentSize().height

10\cc. cc.PointMake 写成cc.p

11\菜单的写法举例

     var item1 = cc.MenuItemImage.create(s_pathB1,s_pathB2, this.onBackCallback, this);

        var item2 = cc.MenuItemImage.create(s_pathR1,s_pathR2, this.onRestartCallback, this);

        var item3 = cc.MenuItemImage.create(s_pathF1,s_pathF2, this.onNextCallback, this);


        var menu = cc.Menu.create(item1, item2, item3);


        menu.setPosition(0,0);

        item1.setPosition(s.width / 2 -item2.getContentSize().width * 2, item2.getContentSize().height / 2);

        item2.setPosition(s.width / 2, item2.getContentSize().height/ 2);

        item3.setPosition(s.width / 2 +item2.getContentSize().width * 2, item2.getContentSize().height / 2);


       this.addChild(menu, 1);





。。。。。。

onBackCallback:function (sender) {

},

    onRestartCallback:function(sender) {

},

    onNextCallback:function (sender){

}

12\jsb v2.0 按帧播放动画 

var animation = cc.Animation.create();
         for (var i = 1; i < 15; i++) {
             varframeName = "res/Images/grossini_dance_" + ((i < 10) ?("0" + i) : i) + ".png";
            animation.addSpriteFrameWithFile(frameName);
         }
         animation.setDelayPerUnit(2.8 / 14);
        animation.setRestoreOriginalFrame(true);

        var action =cc.Animate.create(animation);
        this._grossini.runAction(cc.Sequence.create(action, action.reverse()));

13\jsb V2.0plist播放动画 

caoAction:function(){
         var cache =cc.SpriteFrameCache.getInstance();
        cache.addSpriteFrames(plist_MainMenu_cao,img_MainMenu_cao);
         var cao =cc.Sprite.createWithSpriteFrame(cache.getSpriteFrame("Hy_cao_1.png"));
        cao.setPosition(cc.p(776,768-703.5));
         this.addChild(cao,5);
         var animFrame = [];
         for(var a = 1; a < 5; a++){
             var str ="Hy_cao_"+ a +".png";
            animFrame.push(cache.getSpriteFrame(str));
         }
         var animation =cc.Animation.create(animFrame,0.8);
        cao.runAction(cc.RepeatForever.create(cc.Sequence.create(
            cc.Animate.create(animation),cc.DelayTime.create(3)
         )));
     },


14、背景音乐播放：

cc.AudioEngine.getInstance().setMusicVolume(0.99);

         cc.AudioEngine.getInstance().playMusic(s_mainMainMusic, true);



暂停：cc.AudioEngine.getInstance().pauseMusic();

恢复：cc.AudioEngine.getInstance().resumeMusic();

音效播放

var s =cc.AudioEngine.getInstance().playEffect(s_buttonEffect);

停止：

cc.AudioEngine.getInstance().stopEffect(s_buttonEffect);

15、显示和隐藏 sender.setVisible(false);使能与否backbar.setEnabled(false);

16.setScale 分开写 setScaleX和setScaleY
```
