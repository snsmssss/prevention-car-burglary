The three key components for this solution are NVIDIA Jetson Nano 2GB, AWS cloud(S3, Lambda function, SES) and a smart phone with email configured on it. Jetson Nano has all the built-in CUDA, TRT, Gstreamer is installed and configured. An additional module called jetson-inference should also be configured( instructions for the same is provided in the link). The installation/configuration/execution was done on Ubuntu OS ( we didn't try using container image. That is another option)

When a video from car parking taken around car is streamed into an Object Detector application, it scans the video. If the Object Detector finds any stranger near the car in the night, a bounding box is drawn around the person. The application takes snapshot of the intruder's image and uploads onto AWS S3 bucket. 
As soon as a new object is PUT into the s3 bucket, an AWS service called Lambda gets triggered and it sends an email alert to the Car Owner with the image of intruder. For email, SES service is used.

On AWS S3
create a bucket named PREVENT-CAR-BURGLARY-BUCKET. Refer the same bucket name in detectnet-snap-2s3.py 

Configure Lambda function to send email to YOUR-EMAIL-ID

Configure to receive emails on your smart phone

Configure your AWS profile on jetson nano

Launch the following script on jetson nano

./detectnet-snap-2s3.py CarParking-II-2022-03-05-11PM.mp4 -threshold=0.5 --input-flip=clockwise

Additional Information

For Jetson AI Fundamentals - S3E4 and  Object Detection Inference, watch the following Tutorial video

https://youtu.be/obt60r8ZeB0?list=PL5B692fm6--uQRRDTPsJDp4o0xbzkoyf8

For using the videoSource/videoOutput API

https://github.com/dusty-nv/jetson-inference/blob/master/docs/detectnet-example-2.md
 
https://github.com/dusty-nv/jetson-inference/blob/master/python/examples/my-detection.py
