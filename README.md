1. albumentations supports uint8 and float32 inputs. For the latter, all values must lie in the range [0.0, 1.0]. And should be of shape (H,W,C)
2. need to normalize image after augmentation as it changes mean and stds
3. torch.conv2d expects (N,C,H,W)
4. F.affine_grid(theta, size) theta is backward matrix that takes target coordinates and outputs source coordinates. And the target values lies in the range [-1,1]
5. F.grid_sample(input, grid, mode='bilinear', padding_mode='zeros'), grid specifies the sampling pixel locations normalized by the input spatial dimensions. Therefore, it should have most values in the range of [-1, 1]. For example, values x = -1, y = -1 is the left-top pixel of input, and values x = 1, y = 1 is the right-bottom pixel of input. 
6. MaskRCNN data: return [img1,img2...], [target1,target2...]  
use collate_fn in DataLoader  
> def collate_fn(batch):
>     return tuple(zip(*batch))
img is a tensor of shape (C,H,W) in [0,1] range  
target is a dict with:  
                      "boxes"  : [[x1,y1,x2,y2],[],...[]] of shape (N,4)  
                      "labels" : [c1,c2,...] of shape (N,)  
                      "masks"  : of shape (N,h,w) for each n, it is a array of 0 and 1.  

