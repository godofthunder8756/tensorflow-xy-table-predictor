# Tensorflow XY Table Predictor
A small demonstration of Google's Tensorflow being trained on a table of xy values to establish a correlation used to predict future points.

Dependancies:
tensorflow
numpy
keras

How it works:
We are feeding the table data into the Keras model. The input_shape=[1] just means we are inputing the data in individual increments. 
                    
                    model = tf.keras.Sequential([keras.layers.Dense(units=1, input_shape=[1])])
                    
This is where we set the goals for Tensorflow. We want SGD, an optimizer that implements stochastic gradient descent, with support for
momentum, learning rate decay, and Nesterov momentum. The momentum dampens oscillations, narrowing out pattern. 

                    model.compile(optimizer='sgd', loss='mean_squared_error')
 
Our x values and y values go into two seperate arrays. An array is a matrix with the demensions of 1*n, where n is the number of values.
It is important the x and y have an equal amount of values that correspond respectively. Larger the data, the better!
                  
                    xs = np.array([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], dtype=float)
                    ys = np.array([-2.0, 1.0, 4.0, 7.0, 10.0, 13.0], dtype=float)
                    
Simple command-line input for the number of time we want Tensorflow to run self-refine its "correlations" between the given data.
More indepth, it is tweaking the "weights" and "biases" (which are initially randomly assigned) in order to better suit the data.
Most of the time you will see that the percent error is decreasing and only occasionaly increases. It's like tuning a guitar. I like to 
use 500-1000 trials. 

                   trialtimes = int(input("Number of Trials")) 
                   model.fit(xs, ys, epochs=trialtimes)
Finally, enter the number you predicted!

                    predict = int(input("Predict Number:")) 
                    print(model.predict([predict]))

If I enter "10" is would expect 30.999998. Remeber limits from calculus? If you want a whole number, I would advise using a round()
function on the print() command like so:

                  print(round(model.predict([predict])))


See it in action at:
https://drive.google.com/file/d/1P5-vDL67ZaEKlWZfeHD7IwRVZ0Y7-qLC/view?usp=sharing
