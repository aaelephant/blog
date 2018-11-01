#Cocopods管理开源项目（最后有UI frame和bounds区别）
[http://www.veryitman.com/page/2/](http://www.veryitman.com/page/2/)

1. 实现UIScrollView 嵌套UICollectionView 或UITableView 滑动上去时，把头部顶上去效果；UITableView会和UIScrollView滑动冲突，在自定义UIScrollView中实现
    //与子控件同时响应手势滑动
    - (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldRecognizeSimultaneouslyWithGestureRecognizer:       (UIGestureRecognizer *)otherGestureRecognizer {
        return YES;
    }
  方法可以解决问题 .
