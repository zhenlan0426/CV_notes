1. albumentations supports uint8 and float32 inputs. For the latter, all values must lie in the range [0.0, 1.0]. And should be of shape (H,W,C)
2. need to normalize image after augmentation as it changes mean and stds
3. torch.conv2d expects (N,C,H,W)
4. F.affine_grid(theta, size) theta is backward matrix that takes target coordinates and outputs source coordinates. And the returned values lies in the range [-1,1]
