# StereoConvNet
Stereo fully convolutional neural network for depth map prediction from stereo images. The network is implemented using 
the nn library Lasagne, and training-time/over-fitting are reduced significantly with the help of the recently developed Batch normalization technique (http://arxiv.org/abs/1502.03167).

The network is fully convolutional, and takes a couple of grayscale stereoscopic images concatenated along the channel axis,
and ouputs  a single image representing the depth map. 

The traing/validation sets are created using the random virtual 3d scene generator (see https://github.com/LouisFoucard/DepthMap_dataset) that looks as follows:

Example scene:

![alt tag](https://raw.github.com/LouisFoucard/DepthMap_dataset/master/StereoImages/Stereoscopic_190.png)

and corresponding Depth map:

![alt tag](https://raw.github.com/LouisFoucard/DepthMap_dataset/master/Depth_map/DepthMap_190.png)


The objective function used here is Eulerian distance. 

The architecture is roughly as follows:

Input layer (batch_size x 2 x width x height)

conv1 (batch_size x 16 x width x height)

maxpool1 (batch_size x 16 x width/2 x height/2)

conv2 (batch_sizex 32 x width/2 x height/2)

maxpool2  (batch_size x 32 x width/4 x height/4)

conv3 (batch_size x 64 x width/4 x height/4)

maxool3 (batch_size x 64 x width/8 x height/8)

conv4 (batch_size x 128, x width/8 x height/8)

deconv1 (batch_size x 32, x width/8 x height/8)

upscale1 (batch_size x 32 x width/4 x height/4)

deconv2 (batch_size x 16, x width/4 x height/4)

upscale2 (batch_size x 16 x width/2 x height/2)

deconv3(batch_size x 8 x width/2 x height/2)

upscale3 (batch_size x 8 x width x height)

deconv4  (batch_size x 1 x width x height)

