# VideoProcessing-YOLOV3
Additional Task: Objects Detection in Videos 

# YOLO Approach 
For computer vision enthusiasts, YOLO (You Only Look Once) is an extremely popular real-time object detection concept since 
its very fast and has great performance.

The steps include:
1) Prepare YoloV3 and LoadModel
First clone Ultralytics YoloV3 Repository then import common packages and repo’s function

2) Set Argument Parser, initialize devices (CPU / CUDA), initialize the YOLO model then load weight.

3) Predict Object Detection on Video
Next, we will read the video file and rewrite the video with objects bounding boxes. Following 3 GitHub Gist is part of a function predict_one_video that will be used at the end.

4) Start looping each frame on the video to get predictions.

The image size for this model is 416. A function name letterbox is resizing the image and give padding to image hence one of width or height becomes 416 and the other less than equal 416 but still divisible by 32
The second part is we turn the image into RGB format and put channels in the first dimension (C,H,W). Put the image data into the device (GPU or CPU) and scale the pixel from 0-255 to 0-1 . Before we put the image into the model, we use the function img.unsqeeze(0) because we have to reformat image into 4 dimensions (N,C,H,W) which N is the number of images which is 1 in this case.
After preprocessing the image, we put it into the model to get prediction boxes. But the predictions have a lot of boxes so we need non-maximum suppression to filter and merge the boxes.

5) Draw Bounding Box and Label then Write Video
We loop all the prediction (pred) after NMS to draw the box, but the image is already resized into 416 pixels, we need to scale it back into original size using the function scale_coords then we draw the box using the function plot_one_box

6) Show Video on Colab
The video is written as Mp4 Format on function predict_one_video after saved as Mp4 we compress into h264so the video can be played on Google Colab / Jupyter directly.

7) Show Raw Video
We show video using IPython.display.HTML with 400 width pixels. The video is read using binary

8) Compress and Show Processed Video
The output of OpenCV video writer is an Mp4 video with size 3 times larger than the original video, and it cannot be displayed on Google Colab using the same way, one of the solutions is we do the compression (source)
We compress Mp4 video to h264 usingffmpeg -i {save_path} -vcodec libx264 {compressed_path}

# Output
<img width="1440" alt="Screen Shot 2020-07-25 at 5 04 46 PM" src="https://user-images.githubusercontent.com/50755701/88459161-e8404400-ce9b-11ea-964b-add353f3b3e8.png">
<img width="1275" alt="Screen Shot 2020-07-25 at 5 26 25 PM" src="https://user-images.githubusercontent.com/50755701/88459174-f9895080-ce9b-11ea-93a7-a56a39b0b800.png">
