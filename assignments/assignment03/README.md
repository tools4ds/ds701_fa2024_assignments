# Assignment 03

Assignment 3 released on Probability, Statistics and Distances.
Here is the [notebook](./assignment3.ipynb).

### Special Note for Colab Users

If you are doing this homework on Colab, you will have to take these 3 extra steps:

1. copy this [zipped test folder](./hw3_tests.rar)
   to your Colab local storage<br>
2. In colab run the following commands, <br>
   !pip install rarfile<br>
   !apt-get install unrar<br>
3. Copy the below code and run it in a cell after the pip installations:<br>
   import rarfile<br>
   import os<br>
   rar_file = 'hw3_tests.rar'<br>
   with rarfile.RarFile(rar_file) as rf:<br>
   &nbsp;&nbsp;&nbsp;&nbsp;rf.extractall('test')<br>
5. Add another code cell with `!pip install otter-grader`

The last `grader.export` cell will give you an error, but you should be able to
simply run all cell (except that last one) download your notebook from Colab
and submit the `.ipynb` directly to Gradescope.

Good luck! And reach out on Piazza with any questions or issues.
