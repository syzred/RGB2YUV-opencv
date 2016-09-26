# RGB2YUV-opencv
One C++ project that transfer RGB to YUV with OpenCV lib.

#include <opencv.hpp>
using namespace cv;

int main()
{
	IplImage *src = cvLoadImage("Lena.jpg", 1);//原图　
	IplImage *dst_gray = cvCreateImage(cvGetSize(src), src->depth, 1);//灰度图
	IplImage *dst_image = cvCreateImage(cvGetSize(src), 32, src->nChannels);
	IplImage *src_image_32 = cvCreateImage(cvGetSize(src), 32, src->nChannels);  //这两个图需要是32浮点位的，因为对原图进行归一化后得到的是浮点数　　
	cvConvertScale(src, src_image_32, 1.0 / 255.0, 0);//将原图RGB归一化到0-1之间　　

	cvCvtColor(src, dst_gray, CV_BGR2GRAY);//得到灰度图　　
	cvCvtColor(src_image_32, dst_image, CV_BGR2YUV);//得到HSV图

	// create a window
	cvNamedWindow("mainWin", CV_WINDOW_AUTOSIZE);
	cvMoveWindow("mainWin", 100, 100);

	// show the image
	cvShowImage("mainWin", dst_image);

	waitKey(6000);
	return 0;
}
