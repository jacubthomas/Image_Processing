CSCI 103 Image Filtering Programming Assignment 

Name: Jacob Harrington

Email Address: jharring@usc.edu

Answer the questions posed in the writeup below.

NOTE: It is helpful if you write at most 80 characters per line,
and avoid including special characters, so we can read your responses.

Please summarize the help you found useful for this assignment, which
may include office hours, discussion with peers, tutors, et cetera.
Saying "a CP on Tuesday" is ok if you don't remember their name.
If none, say "none".

: CPs in SAL 

================================ Questions ==================================

1. Padding design: If we restrict the size of the Gaussian kernels to odd 
integers between 3 and 11 inclusive, and we only allow 256x256 pixel images, 
what is the size of the largest padded image needed to handle padding with 
any kernel size? At what index will the upper-left pixel of the original 
image be placed in the padded image (answer in terms of N, the kernel size)? 
At what index in the padded array will the lower-right pixel of the original 
image be placed?

: a) The largest padded image would be made to handle an 11*11 kernel, which
  would extend the image by 10 pixels in each row / column resulting in a
  266*266 size image. This is because the kernel would need to be
  centered on values of the image border. b) The upper left pixel would be
  placed in the padded image at [(0 + N/2),(0 + N/2)] of course relying on
  integer division for N/2. c) The upper left pixel would be be placed in 
  the padded image at [(256 + N/2),(256 + N/2)].

2. Kernel Design: Manually compute the raw and normalized Gaussian kernels 
for N=3, sigma=2. Use 4 decimal places. Discuss what would happen to the 
image if we used the raw kernel values.

:   RAW GAUSS                                                                                                              
    0.7788 0.8825 0.7788                                                                                             
    0.8825      1 0.8825                                                                                            
    0.7788 0.8825 0.7788                                                                                             
    NORMAL GAUSS                                                                                                           
    0.1019 0.1154 0.1019                                                                                             
    0.1154 0.1308 0.1154                                                                                             
    0.1019 0.1154 0.1019

    b) If we used the values of the raw gauss, the sum of the raw kernel
    values is > 1, and thereby, would make the image overall brighter. 
   

3. Experimenation:  Provide the results for ALL experiments listed in the
                    writeup.

: 1) Holding N constant, at say 3, and varying sigma values from 0.1 - 10
  I see that the image blur grows in intensity with relation to sigma.
  When sigma is constant, at say 2, and varying N size from 3 - 11, the
  image blur also grows in intensity with relation to N, however much
  more so than varying sigma. In addition, keeping sigma low, say 0.1,
  and again varying N from 3 - 11, I see no discernible difference in
  blur intensity. My hypothesis is that a blur with an appreciable value
  for sigma, can be further intensified by larger kernel sizes as the
  number of computations performed on each pixel grows with the kernel.
  2) The sobel filter works as an edge detector. It compares the values
  of adjacent pixels to look for objects in an image. if the pixel values
  don't match, there must be two objects; if they do, there is only one
  object in the kernel focus.
  3) No, in doing so you do not get back the original image. Gaussian
  blurs an input image based on a variance of sigma and a kernel size N
  to an output image. To implement an unsharp mask, requires an input
  image be blurred into a temp image container, which is then used to
  to create a detail map stored in yet another seperate image container.
  Finally, the output image is the result of the original image + the
  detail map multiplied by a value alpha; this is all done pixel-
  by-pixel. Trying to recover an original image from a blurred using an 
  unsharp mask will fail as you will be adding a detail map derived from
  blurring a blurred image to a blurred image.


4. Express in mathematical terms how the number of calculations your 
 program performs grows with the size, N, of the kernel.

: As the kernel grows with size, the number of calculations grows. This
  growth in the number of elements in the kernel requires that more
  values must be processed with the raw gauss equation, and further,
  more values will be summed to normalize the raw gauss kernel. Thus,
  The calculation can be summed by the (N+k)^2 - N^2 where k is the
  constant for change kernel size and N is the value of original size.
  
  
================================ Remarks ====================================

Filling in anything here is OPTIONAL.

Approximately how long did you spend on this assignment?

: Maybe 20 hours. Much longer than other PAs!

Were there any specific problems you encountered? This is especially useful to
know if you turned it in incomplete.

: There is a substantial jump in the nature of equations implemented. Another,
  in processing color vice monochromatic images. The final unresolved issue in
  my code deals with line 140 where I changed temp to a double[] in place of 
  int[]. No matter the casts I made in convolve, I could not work around this
  with temp as an int. I then tried using an additional temp2 double[] for the
  calculations, leaving temp as int, and still valgrind would not let up.

Do you have any other remarks?

: Perhaps, in the future going through more complex equation implementation
  examples in class leading up to this PA will help.
