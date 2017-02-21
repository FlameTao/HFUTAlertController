# HFUTAlertController

HFUTAlertController是一个基于转场动画，封装了一些类似于UIAlertController的一些操作。

## 说明

### 展示

<img src="http://www.flametao.cn/2017/02/21/HFUTAlertController/default_double.gif" style="zoom:50%" />
<img src="http://www.flametao.cn/2017/02/21/HFUTAlertController/success_single.gif" style="zoom:50%" />
<img src="http://www.flametao.cn/2017/02/21/HFUTAlertController/failure_single.gif" style="zoom:50%" />
<img src="http://www.flametao.cn/2017/02/21/HFUTAlertController/info_single.gif" style="zoom:50%" />

### 使用的三方库

[**pop**](https://github.com/facebook/pop)：facebook开源的游戏级别的动画引擎，相当好用，点击链接了解详情

[**Masonry**](https://github.com/SnapKit/Masonry)：封装的非常好用的布局操作，相当方便，点击链接了解详情



## 使用

### 开始

首先需要导入上面所说的三方库，然后直接下载文件导入项目

接着包含头文件

```objective-c
#import "HFUTAlert.h"
```

假设在一个`ViewController`上弹出`AlertController`，需要`ViewController`遵从`<UIViewControllerTransitioningDelegate>`协议，并实现下面两个方法。

```objective-c
//ViewController.m
@interface ViewController () <UIViewControllerTransitioningDelegate>
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    // Do any additional setup after loading the view.
}
#pragma mark - UIViewControllerTransitioningDelegate
- (id<UIViewControllerAnimatedTransitioning>)animationControllerForPresentedController:(UIViewController *)presented presentingController:(UIViewController *)presenting sourceController:(UIViewController *)source {
    return [HFUTPresentingAnimator new];
}

- (id<UIViewControllerAnimatedTransitioning>)animationControllerForDismissedController:(UIViewController *)dismissed {
    return [HFUTDismissingAnimator new];
}
@end
```

假设点击一个`ViewController`里的按钮弹出`Alert`

```objective-c
- (IBAction)button:(id)sender {
    HFUTAlertController * alert = [HFUTAlertController alertWithTitle:@"XXOO" message:@"xxxxxoooooo" style:AlertStyleInfoWithDoubleButton];
    alert.transitioningDelegate = self; //！！！一定要有
    [self presentViewController:alert animated:YES completion:nil];
}
```

如果`ViewController`继承NavigationController，就使用这个方法弹出

```objective-c
[self.navigationController presentViewController:alert animated:YES completion:nil];
```

### 操作

设置确认和取消按钮的响应事件，在`presentViewController`之前通过下面操作

```objective-c
[alert setDefaultCompletion:^{
        ...
    }];
[alert setCancelCompletion:^{
  ...
}]
```

更改按钮的名字

```objective-c
[alert setDefaultButtonTitle:title];
[alert setCancelButtonTitle:title];
```

### 了解

选择不一样的style又不一样风格的Alert

- AlertStyleDefaultWithSingleButton
- AlertStyleDefaultWithDoubleButton
- AlertStyleSuccessWithSingleButton
- AlertStyleFailureWithSingleButton
- AlertStyleInfoWithSingleButton