Download Link: https://assignmentchef.com/product/solved-csgy6643-assignment-3
<br>
<strong>Hint for implementation</strong>: Most image processing <u>require using float or double type for image arrays</u>. You can map those images back to integer at the very end of the processing for display purposes, and during this operation you can also optimally scale and shift the result to [0..255] after calculation of minimum and maximum intensities across the resulting image.




<h1>1)  Convolution and Derivative Filters</h1>

<strong> </strong>

<strong>Convolution: </strong>Implement 2D convolution (denoted *) without the use of built in functions. Your function will take as input two 2D arrays, a filter <em>f </em>and an image <em>I, </em>and return <em>f</em><em>I</em>. You can handle the boundary of <em>I </em>in any reasonable way of your choice, such as padding with zeros based on the size of the filter <em>f</em>. You are free to make use of any part of your previous indexing implementation.










def convolution(f, I):

<em># Handle boundary of I, e.g. pad I according to size of f </em>

<em>       </em>

<em># Compute im_conv = f*I </em>

<em>      </em>return im_conv




<strong>Derivative Filters: </strong>Using the example image ‘cameraman.png’




<ul>

 <li>Denoise the image with a Gaussian filter. You may use the code from the in class demo to create the Gaussian filter, but <u>you must use your own implementation of convolution</u>.</li>

 <li>Compute derivative images (with respect to x and with respect to y) using the separable derivative filter of your choice, e.g. [-1 0 1] and [-1 0 1]<sup>T</sup>. <u>You can hardcode the derivative filter, but use your</u> <u>implementation of convolution</u>.</li>

 <li>Compute the gradient magnitude image.</li>

 <li>Create binary edge images from the gradient magnitude image using several thresholds</li>

</ul>




In your report, introduce how the derivative filter is a discrete approximation of a derivative. Show all results and discuss the outcome of various thresholds.

<h1>2)  Cross-correlation and Template Matching</h1>










The uploaded image ‘<em>multiplekeys.png</em>’ is a single image containing multiple instances of keys.




Perform the following steps:

<ul>

 <li>Threshold the original key image so that the background is [0.0] and keys appear as [1.0]. You should have a binary image with only [0.0] (background) and [1.0] (keys).</li>

 <li>Choose your favorite key and crop with a narrow boundary. Use this image as your template.</li>

 <li>Modify your template by setting background pixels to [-1.0], so that you have [+1.0] for the key and [-1.0] for background. The reason for creating a signed template is improved matching performance.</li>

 <li>Implement cross-correlation with the binary input image and your new signed template image.</li>

 <li>Please recall that this results in a peak (maximum) if the template matches the specific image region which you selected for your template.</li>

 <li>Do a pass through the correlation image to detect the maximum peak value and its (x,y) location. You may mark this location with an overlay of a circle or just manually painting an arrow or similar. Discuss if this location matches your expectation. Discuss the appearance and cause of other local peaks, and how they compare to the global peak.</li>

</ul>




In your report, show the original image, peak image (output of cross-correlation), and your template which was used for correlation.

<h1>3)  Image Panoramas</h1>

<strong> </strong>

An image panorama is created by stitching together several images. The images must be taken under certain criteria: the camera cannot undergo translation between pictures; <u>only rotational transformations are allowed</u>.
















If you have ever tried to create a panorama by hand by cutting out pictures and taping them together you know that it doesn’t work very well. Translation and rotation are not sufficient to align the two images together. <u>In</u> <u>order for the panorama to look right, one of the images must also be transformed/warped.</u>




A key observation is that images taken under the aforementioned criteria are equivalent under a <u>perspective</u> <u>projection</u>. We can take corresponding points between two images and create a linear system. In general, we choose many correspondences so that the system is overconstrained, and the transformation is found by linear least squares.

<strong> </strong>

<u>The following equations detail how to set up the matrix system:</u>










<ul>

 <li>Take two photos which overlap and differ only in rotation, e.g. similar to the example images above.</li>

 <li><u>Implement an image panorama for the case of 2 images (a source and a target)</u>. The algorithm is:

  <ul>

   <li>Define corresponding points between the two images (these are pixel coordinates which you can find by hovering your mouse in a paint program, or found in any manner of your choice).</li>

   <li>Using the corresponding points, construct the known matrix and vector shown above. <u>Note that</u> <u>this is similar to our affine example but with a different matrix structure</u>.</li>

   <li>Solve for parameters P with linear least squares (e.g. use np.linalg.lstsq or similar).</li>

   <li>Using the found parameters P, transform the target image. <u>You must implement the</u> <u>transformation yourself, but you may use any code from the demos</u>. You can use any interpolation of your choice.</li>

   <li>Combine the source and transformed target <u>together on the same canvas</u>. You can handle the area of overlap in anyway you choose (simplest is to always overwrite the grey values in the canvas image). <u>Don’t worry if your panorama has an obvious seam</u>.</li>

  </ul></li>

 <li>Compare results using 4, 5, 6, and 7 corresponding points.</li>

</ul>




Include all results and discussion in your report. <u>Remember your report needs to be a standalone document</u> <u>that someone outside of class can follow.</u>