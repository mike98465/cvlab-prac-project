# cvlab_prac_project
Test model with different parameters or adjust its structure
--------------------------------------------------------------------------


I've test model with:

*   select epoch length (train longer)
*   test with different type of loss function
*   lr decay or lower lr
*   use SGD instead of Adam
*   use deeper one & adjust model structure
*   higher resolution image

1.select epoch length (train longer)
-------------------------------------------------------------------------

I've tried epoch length with 20, 25, 30, 35, 40. I found that 35 is better, and if I train
model for 40 epoch, its mse behaved unstable and didn't decrease anymore. ( with lr = 1e-4)


2.test with different type of loss function
-------------------------------------------------------------------------

I've tried MSE, BCE, BCEWithLogitsLoss, SmoothL1Loss function before, but their performance
were all worse than the L1Loss. Hence, I didn't modify this part of the orginal code. 


3.lr decay or lower lr
-------------------------------------------------------------------------

+ lr decay:
I have used lr_scheduler to implement the lr decay, and I found that the performance on mse
is much better than the previous fixed lr. (1e-4)

    $  optimizer = torch.optim.Adam(model.parameters()) #modified
    $  scheduler = torch.optim.lr_scheduler.StepLR(optimizer, step_size=10, gamma=0.1) #added
    $  scheduler.step() #added

+ lower lr:
I tried lr = 1e-5, but it converged too slow and I just gave up this experience.


4.use SGD instead of Adam
------------------------------------------------------------------------

SGD optimizer didn't perform better than the Adam.


5.use deeper one & adjust model structure
------------------------------------------------------------------------

try to use deeper model by:

    $  ConvBlock(64, 128), #added
    $  nn.MaxPool2d((2, 2)), #added
    $  x = self.act1(self.bn2(self.conv2(x))) #added

its mse performance didn't seem better.


6.higher resolution image
------------------------------------------------------------------------

code adjusted by:

    $  img = img.resize((400, 240)) #modified
    $  img_b = torch.rand(16, 3, 400, 240).to(device) #modified 

its mse performance didn't seem better.
