{
 "metadata": {
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.4-final"
  },
  "orig_nbformat": 2,
  "kernelspec": {
   "name": "python38464bit5ff9940120d14a77bacde899b84cd449",
   "display_name": "Python 3.8.4 64-bit",
   "language": "python"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2,
 "cells": [
  {
   "source": [
    "# Linear algebra\n",
    "\n",
    "_Import of panda libraries_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "metadata": {},
   "outputs": [],
   "source": [
    "import re, math, random \n",
    "import matplotlib.pyplot as plt \n",
    "import numpy as np\n",
    "from collections import defaultdict, Counter\n",
    "from functools import partial, reduce"
   ]
  },
  {
   "source": [
    "## Operating on vectors\n",
    "_Introduction of vectors (examples)_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "metadata": {},
   "outputs": [
    {
     "output_type": "stream",
     "name": "stdout",
     "text": [
      "v vector =  [1, 2]  w vector =  [2, 3]\n"
     ]
    }
   ],
   "source": [
    "v = [1,2]\n",
    "w = [2,3]\n",
    "print('v vector = ', v, ' w vector = ', w)"
   ]
  },
  {
   "source": [
    "_Definition of basic operations on vectors:_\n",
    "\n",
    "_\n",
    "1. addition\n",
    "2. subtraction\n",
    "3. scalar multiplication\n",
    "4. dot product\n",
    "_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 58,
   "metadata": {},
   "outputs": [],
   "source": [
    "def vector_add(v, w):\n",
    "    return [v_i + w_i for v_i, w_i in zip(v,w)]\n",
    "\n",
    "def vector_subtract(v, w):\n",
    "    return [v_i - w_i for v_i, w_i in zip(v,w)]\n",
    "\n",
    "def scalar_multiply(c, v):\n",
    "    return [c * v_i for v_i in v]\n",
    "\n",
    "def dot_product(v, w):\n",
    "    return sum(v_i * w_i for v_i, w_i in zip(v, w))"
   ]
  },
  {
   "source": [
    "_Now, I am checking out the functions:_  "
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "metadata": {},
   "outputs": [
    {
     "output_type": "stream",
     "name": "stdout",
     "text": [
      "sum of vectors\n"
     ]
    },
    {
     "output_type": "execute_result",
     "data": {
      "text/plain": [
       "[3, 5]"
      ]
     },
     "metadata": {},
     "execution_count": 59
    }
   ],
   "source": [
    "print('sum of vectors')\n",
    "vector_add(v,w)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 60,
   "metadata": {},
   "outputs": [
    {
     "output_type": "stream",
     "name": "stdout",
     "text": [
      "difference of vectors\n"
     ]
    },
    {
     "output_type": "execute_result",
     "data": {
      "text/plain": [
       "[-1, -1]"
      ]
     },
     "metadata": {},
     "execution_count": 60
    }
   ],
   "source": [
    "print('difference of vectors')\n",
    "vector_subtract(v,w)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 61,
   "metadata": {},
   "outputs": [
    {
     "output_type": "stream",
     "name": "stdout",
     "text": [
      "product of multiplication of vector v with scalar, e.g. 3\n"
     ]
    },
    {
     "output_type": "execute_result",
     "data": {
      "text/plain": [
       "[3, 6]"
      ]
     },
     "metadata": {},
     "execution_count": 61
    }
   ],
   "source": [
    "print('product of multiplication of vector v with scalar, e.g. 3')\n",
    "scalar_multiply(3, v)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 62,
   "metadata": {},
   "outputs": [
    {
     "output_type": "stream",
     "name": "stdout",
     "text": [
      "dot product of vectors\n"
     ]
    },
    {
     "output_type": "execute_result",
     "data": {
      "text/plain": [
       "8"
      ]
     },
     "metadata": {},
     "execution_count": 62
    }
   ],
   "source": [
    "print('dot product of vectors')\n",
    "dot_product(v,w)"
   ]
  },
  {
   "source": [
    "_Calculation of vector length_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 63,
   "metadata": {},
   "outputs": [],
   "source": [
    "def sum_of_squares(v):\n",
    "    return dot_product(v, v)\n",
    "\n",
    "def magnitude(v):\n",
    "    return math.sqrt(sum_of_squares(v))"
   ]
  },
  {
   "source": [
    "_I use \"round\" function to reduce number of decimal places_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 64,
   "metadata": {},
   "outputs": [
    {
     "output_type": "execute_result",
     "data": {
      "text/plain": [
       "2.24"
      ]
     },
     "metadata": {},
     "execution_count": 64
    }
   ],
   "source": [
    "round(magnitude(v),2)"
   ]
  },
  {
   "source": [
    "_Drawing of vectors starting at the same point_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "metadata": {},
   "outputs": [
    {
     "output_type": "display_data",
     "data": {
      "text/plain": "<Figure size 432x288 with 1 Axes>",
      "image/svg+xml": "<?xml version=\"1.0\" encoding=\"utf-8\" standalone=\"no\"?>\r\n<!DOCTYPE svg PUBLIC \"-//W3C//DTD SVG 1.1//EN\"\r\n  \"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd\">\r\n<!-- Created with matplotlib (https://matplotlib.org/) -->\r\n<svg height=\"248.518125pt\" version=\"1.1\" viewBox=\"0 0 370.942187 248.518125\" width=\"370.942187pt\" xmlns=\"http://www.w3.org/2000/svg\" xmlns:xlink=\"http://www.w3.org/1999/xlink\">\r\n <metadata>\r\n  <rdf:RDF xmlns:cc=\"http://creativecommons.org/ns#\" xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:rdf=\"http://www.w3.org/1999/02/22-rdf-syntax-ns#\">\r\n   <cc:Work>\r\n    <dc:type rdf:resource=\"http://purl.org/dc/dcmitype/StillImage\"/>\r\n    <dc:date>2021-01-05T16:09:59.699829</dc:date>\r\n    <dc:format>image/svg+xml</dc:format>\r\n    <dc:creator>\r\n     <cc:Agent>\r\n      <dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title>\r\n     </cc:Agent>\r\n    </dc:creator>\r\n   </cc:Work>\r\n  </rdf:RDF>\r\n </metadata>\r\n <defs>\r\n  <style type=\"text/css\">*{stroke-linecap:butt;stroke-linejoin:round;}</style>\r\n </defs>\r\n <g id=\"figure_1\">\r\n  <g id=\"patch_1\">\r\n   <path d=\"M 0 248.518125 \r\nL 370.942187 248.518125 \r\nL 370.942187 0 \r\nL 0 0 \r\nz\r\n\" style=\"fill:none;\"/>\r\n  </g>\r\n  <g id=\"axes_1\">\r\n   <g id=\"patch_2\">\r\n    <path d=\"M 28.942188 224.64 \r\nL 363.742188 224.64 \r\nL 363.742188 7.2 \r\nL 28.942188 7.2 \r\nz\r\n\" style=\"fill:#ffffff;\"/>\r\n   </g>\r\n   <g id=\"Quiver_1\">\r\n    <path clip-path=\"url(#pbbc23f4b63)\" d=\"M 195.347354 115.15411 \r\nL 221.934346 80.619609 \r\nL 219.17879 80.082663 \r\nL 229.822188 72.432 \r\nL 225.147789 84.678001 \r\nL 223.924013 82.151389 \r\nL 197.337021 116.68589 \r\nL 195.347354 115.15411 \r\n\" style=\"fill:#ff0000;\"/>\r\n    <path clip-path=\"url(#pbbc23f4b63)\" d=\"M 195.658353 114.867075 \r\nL 253.142032 77.533589 \r\nL 250.721437 76.111575 \r\nL 263.302188 72.432 \r\nL 254.824447 82.429122 \r\nL 254.509701 79.639438 \r\nL 197.026022 116.972925 \r\nL 195.658353 114.867075 \r\n\" style=\"fill:#008000;\"/>\r\n   </g>\r\n   <g id=\"matplotlib.axis_1\">\r\n    <g id=\"xtick_1\">\r\n     <g id=\"line2d_1\">\r\n      <defs>\r\n       <path d=\"M 0 0 \r\nL 0 3.5 \r\n\" id=\"mbf443cb931\" style=\"stroke:#000000;stroke-width:0.8;\"/>\r\n      </defs>\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"62.422188\" xlink:href=\"#mbf443cb931\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_1\">\r\n      <!-- −4 -->\r\n      <g transform=\"translate(55.051094 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 10.59375 35.5 \r\nL 73.1875 35.5 \r\nL 73.1875 27.203125 \r\nL 10.59375 27.203125 \r\nz\r\n\" id=\"DejaVuSans-8722\"/>\r\n        <path d=\"M 37.796875 64.3125 \r\nL 12.890625 25.390625 \r\nL 37.796875 25.390625 \r\nz\r\nM 35.203125 72.90625 \r\nL 47.609375 72.90625 \r\nL 47.609375 25.390625 \r\nL 58.015625 25.390625 \r\nL 58.015625 17.1875 \r\nL 47.609375 17.1875 \r\nL 47.609375 0 \r\nL 37.796875 0 \r\nL 37.796875 17.1875 \r\nL 4.890625 17.1875 \r\nL 4.890625 26.703125 \r\nz\r\n\" id=\"DejaVuSans-52\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_2\">\r\n     <g id=\"line2d_2\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"129.382188\" xlink:href=\"#mbf443cb931\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_2\">\r\n      <!-- −2 -->\r\n      <g transform=\"translate(122.011094 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 19.1875 8.296875 \r\nL 53.609375 8.296875 \r\nL 53.609375 0 \r\nL 7.328125 0 \r\nL 7.328125 8.296875 \r\nQ 12.9375 14.109375 22.625 23.890625 \r\nQ 32.328125 33.6875 34.8125 36.53125 \r\nQ 39.546875 41.84375 41.421875 45.53125 \r\nQ 43.3125 49.21875 43.3125 52.78125 \r\nQ 43.3125 58.59375 39.234375 62.25 \r\nQ 35.15625 65.921875 28.609375 65.921875 \r\nQ 23.96875 65.921875 18.8125 64.3125 \r\nQ 13.671875 62.703125 7.8125 59.421875 \r\nL 7.8125 69.390625 \r\nQ 13.765625 71.78125 18.9375 73 \r\nQ 24.125 74.21875 28.421875 74.21875 \r\nQ 39.75 74.21875 46.484375 68.546875 \r\nQ 53.21875 62.890625 53.21875 53.421875 \r\nQ 53.21875 48.921875 51.53125 44.890625 \r\nQ 49.859375 40.875 45.40625 35.40625 \r\nQ 44.1875 33.984375 37.640625 27.21875 \r\nQ 31.109375 20.453125 19.1875 8.296875 \r\nz\r\n\" id=\"DejaVuSans-50\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_3\">\r\n     <g id=\"line2d_3\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"196.342188\" xlink:href=\"#mbf443cb931\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_3\">\r\n      <!-- 0 -->\r\n      <g transform=\"translate(193.160938 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 31.78125 66.40625 \r\nQ 24.171875 66.40625 20.328125 58.90625 \r\nQ 16.5 51.421875 16.5 36.375 \r\nQ 16.5 21.390625 20.328125 13.890625 \r\nQ 24.171875 6.390625 31.78125 6.390625 \r\nQ 39.453125 6.390625 43.28125 13.890625 \r\nQ 47.125 21.390625 47.125 36.375 \r\nQ 47.125 51.421875 43.28125 58.90625 \r\nQ 39.453125 66.40625 31.78125 66.40625 \r\nz\r\nM 31.78125 74.21875 \r\nQ 44.046875 74.21875 50.515625 64.515625 \r\nQ 56.984375 54.828125 56.984375 36.375 \r\nQ 56.984375 17.96875 50.515625 8.265625 \r\nQ 44.046875 -1.421875 31.78125 -1.421875 \r\nQ 19.53125 -1.421875 13.0625 8.265625 \r\nQ 6.59375 17.96875 6.59375 36.375 \r\nQ 6.59375 54.828125 13.0625 64.515625 \r\nQ 19.53125 74.21875 31.78125 74.21875 \r\nz\r\n\" id=\"DejaVuSans-48\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-48\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_4\">\r\n     <g id=\"line2d_4\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"263.302188\" xlink:href=\"#mbf443cb931\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_4\">\r\n      <!-- 2 -->\r\n      <g transform=\"translate(260.120938 239.238437)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_5\">\r\n     <g id=\"line2d_5\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"330.262188\" xlink:href=\"#mbf443cb931\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_5\">\r\n      <!-- 4 -->\r\n      <g transform=\"translate(327.080938 239.238437)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n   </g>\r\n   <g id=\"matplotlib.axis_2\">\r\n    <g id=\"ytick_1\">\r\n     <g id=\"line2d_6\">\r\n      <defs>\r\n       <path d=\"M 0 0 \r\nL -3.5 0 \r\n\" id=\"m383df963e4\" style=\"stroke:#000000;stroke-width:0.8;\"/>\r\n      </defs>\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m383df963e4\" y=\"202.896\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_6\">\r\n      <!-- −4 -->\r\n      <g transform=\"translate(7.2 206.695219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_2\">\r\n     <g id=\"line2d_7\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m383df963e4\" y=\"159.408\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_7\">\r\n      <!-- −2 -->\r\n      <g transform=\"translate(7.2 163.207219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_3\">\r\n     <g id=\"line2d_8\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m383df963e4\" y=\"115.92\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_8\">\r\n      <!-- 0 -->\r\n      <g transform=\"translate(15.579688 119.719219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-48\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_4\">\r\n     <g id=\"line2d_9\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m383df963e4\" y=\"72.432\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_9\">\r\n      <!-- 2 -->\r\n      <g transform=\"translate(15.579688 76.231219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_5\">\r\n     <g id=\"line2d_10\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m383df963e4\" y=\"28.944\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_10\">\r\n      <!-- 4 -->\r\n      <g transform=\"translate(15.579688 32.743219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n   </g>\r\n   <g id=\"patch_3\">\r\n    <path d=\"M 28.942188 224.64 \r\nL 28.942188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_4\">\r\n    <path d=\"M 363.742188 224.64 \r\nL 363.742188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_5\">\r\n    <path d=\"M 28.942187 224.64 \r\nL 363.742188 224.64 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_6\">\r\n    <path d=\"M 28.942187 7.2 \r\nL 363.742188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n  </g>\r\n </g>\r\n <defs>\r\n  <clipPath id=\"pbbc23f4b63\">\r\n   <rect height=\"217.44\" width=\"334.8\" x=\"28.942188\" y=\"7.2\"/>\r\n  </clipPath>\r\n </defs>\r\n</svg>\r\n",
      "image/png": "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\n"
     },
     "metadata": {
      "needs_background": "light"
     }
    }
   ],
   "source": [
    "plt.quiver([0, 0], [0, 0], [v[0], w[0]], [v[1], v[1]], angles='xy', scale_units='xy', scale=1, color= ['r', 'g'])\n",
    "plt.xlim(-5, 5)\n",
    "plt.ylim(-5, 5)\n",
    "plt.show()"
   ]
  },
  {
   "source": [
    "_Drawing of vectors one by one_"
   ],
   "cell_type": "markdown",
   "metadata": {}
  },
  {
   "cell_type": "code",
   "execution_count": 90,
   "metadata": {},
   "outputs": [
    {
     "output_type": "display_data",
     "data": {
      "text/plain": "<Figure size 432x288 with 1 Axes>",
      "image/svg+xml": "<?xml version=\"1.0\" encoding=\"utf-8\" standalone=\"no\"?>\r\n<!DOCTYPE svg PUBLIC \"-//W3C//DTD SVG 1.1//EN\"\r\n  \"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd\">\r\n<!-- Created with matplotlib (https://matplotlib.org/) -->\r\n<svg height=\"248.518125pt\" version=\"1.1\" viewBox=\"0 0 370.942187 248.518125\" width=\"370.942187pt\" xmlns=\"http://www.w3.org/2000/svg\" xmlns:xlink=\"http://www.w3.org/1999/xlink\">\r\n <metadata>\r\n  <rdf:RDF xmlns:cc=\"http://creativecommons.org/ns#\" xmlns:dc=\"http://purl.org/dc/elements/1.1/\" xmlns:rdf=\"http://www.w3.org/1999/02/22-rdf-syntax-ns#\">\r\n   <cc:Work>\r\n    <dc:type rdf:resource=\"http://purl.org/dc/dcmitype/StillImage\"/>\r\n    <dc:date>2021-01-05T16:11:08.573973</dc:date>\r\n    <dc:format>image/svg+xml</dc:format>\r\n    <dc:creator>\r\n     <cc:Agent>\r\n      <dc:title>Matplotlib v3.3.2, https://matplotlib.org/</dc:title>\r\n     </cc:Agent>\r\n    </dc:creator>\r\n   </cc:Work>\r\n  </rdf:RDF>\r\n </metadata>\r\n <defs>\r\n  <style type=\"text/css\">*{stroke-linecap:butt;stroke-linejoin:round;}</style>\r\n </defs>\r\n <g id=\"figure_1\">\r\n  <g id=\"patch_1\">\r\n   <path d=\"M 0 248.518125 \r\nL 370.942187 248.518125 \r\nL 370.942187 0 \r\nL 0 0 \r\nz\r\n\" style=\"fill:none;\"/>\r\n  </g>\r\n  <g id=\"axes_1\">\r\n   <g id=\"patch_2\">\r\n    <path d=\"M 28.942188 224.64 \r\nL 363.742188 224.64 \r\nL 363.742188 7.2 \r\nL 28.942188 7.2 \r\nz\r\n\" style=\"fill:#ffffff;\"/>\r\n   </g>\r\n   <g id=\"Quiver_1\">\r\n    <path clip-path=\"url(#p0e6de47c32)\" d=\"M 195.347354 115.15411 \r\nL 221.934346 80.619609 \r\nL 219.17879 80.082663 \r\nL 229.822188 72.432 \r\nL 225.147789 84.678001 \r\nL 223.924013 82.151389 \r\nL 197.337021 116.68589 \r\nL 195.347354 115.15411 \r\n\" style=\"fill:#ff0000;\"/>\r\n    <path clip-path=\"url(#p0e6de47c32)\" d=\"M 229.138353 71.379075 \r\nL 286.622032 34.045589 \r\nL 284.201437 32.623575 \r\nL 296.782188 28.944 \r\nL 288.304447 38.941122 \r\nL 287.989701 36.151438 \r\nL 230.506022 73.484925 \r\nL 229.138353 71.379075 \r\n\" style=\"fill:#008000;\"/>\r\n   </g>\r\n   <g id=\"matplotlib.axis_1\">\r\n    <g id=\"xtick_1\">\r\n     <g id=\"line2d_1\">\r\n      <defs>\r\n       <path d=\"M 0 0 \r\nL 0 3.5 \r\n\" id=\"mc5b05b3048\" style=\"stroke:#000000;stroke-width:0.8;\"/>\r\n      </defs>\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"62.422188\" xlink:href=\"#mc5b05b3048\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_1\">\r\n      <!-- −4 -->\r\n      <g transform=\"translate(55.051094 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 10.59375 35.5 \r\nL 73.1875 35.5 \r\nL 73.1875 27.203125 \r\nL 10.59375 27.203125 \r\nz\r\n\" id=\"DejaVuSans-8722\"/>\r\n        <path d=\"M 37.796875 64.3125 \r\nL 12.890625 25.390625 \r\nL 37.796875 25.390625 \r\nz\r\nM 35.203125 72.90625 \r\nL 47.609375 72.90625 \r\nL 47.609375 25.390625 \r\nL 58.015625 25.390625 \r\nL 58.015625 17.1875 \r\nL 47.609375 17.1875 \r\nL 47.609375 0 \r\nL 37.796875 0 \r\nL 37.796875 17.1875 \r\nL 4.890625 17.1875 \r\nL 4.890625 26.703125 \r\nz\r\n\" id=\"DejaVuSans-52\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_2\">\r\n     <g id=\"line2d_2\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"129.382188\" xlink:href=\"#mc5b05b3048\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_2\">\r\n      <!-- −2 -->\r\n      <g transform=\"translate(122.011094 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 19.1875 8.296875 \r\nL 53.609375 8.296875 \r\nL 53.609375 0 \r\nL 7.328125 0 \r\nL 7.328125 8.296875 \r\nQ 12.9375 14.109375 22.625 23.890625 \r\nQ 32.328125 33.6875 34.8125 36.53125 \r\nQ 39.546875 41.84375 41.421875 45.53125 \r\nQ 43.3125 49.21875 43.3125 52.78125 \r\nQ 43.3125 58.59375 39.234375 62.25 \r\nQ 35.15625 65.921875 28.609375 65.921875 \r\nQ 23.96875 65.921875 18.8125 64.3125 \r\nQ 13.671875 62.703125 7.8125 59.421875 \r\nL 7.8125 69.390625 \r\nQ 13.765625 71.78125 18.9375 73 \r\nQ 24.125 74.21875 28.421875 74.21875 \r\nQ 39.75 74.21875 46.484375 68.546875 \r\nQ 53.21875 62.890625 53.21875 53.421875 \r\nQ 53.21875 48.921875 51.53125 44.890625 \r\nQ 49.859375 40.875 45.40625 35.40625 \r\nQ 44.1875 33.984375 37.640625 27.21875 \r\nQ 31.109375 20.453125 19.1875 8.296875 \r\nz\r\n\" id=\"DejaVuSans-50\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_3\">\r\n     <g id=\"line2d_3\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"196.342188\" xlink:href=\"#mc5b05b3048\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_3\">\r\n      <!-- 0 -->\r\n      <g transform=\"translate(193.160938 239.238437)scale(0.1 -0.1)\">\r\n       <defs>\r\n        <path d=\"M 31.78125 66.40625 \r\nQ 24.171875 66.40625 20.328125 58.90625 \r\nQ 16.5 51.421875 16.5 36.375 \r\nQ 16.5 21.390625 20.328125 13.890625 \r\nQ 24.171875 6.390625 31.78125 6.390625 \r\nQ 39.453125 6.390625 43.28125 13.890625 \r\nQ 47.125 21.390625 47.125 36.375 \r\nQ 47.125 51.421875 43.28125 58.90625 \r\nQ 39.453125 66.40625 31.78125 66.40625 \r\nz\r\nM 31.78125 74.21875 \r\nQ 44.046875 74.21875 50.515625 64.515625 \r\nQ 56.984375 54.828125 56.984375 36.375 \r\nQ 56.984375 17.96875 50.515625 8.265625 \r\nQ 44.046875 -1.421875 31.78125 -1.421875 \r\nQ 19.53125 -1.421875 13.0625 8.265625 \r\nQ 6.59375 17.96875 6.59375 36.375 \r\nQ 6.59375 54.828125 13.0625 64.515625 \r\nQ 19.53125 74.21875 31.78125 74.21875 \r\nz\r\n\" id=\"DejaVuSans-48\"/>\r\n       </defs>\r\n       <use xlink:href=\"#DejaVuSans-48\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_4\">\r\n     <g id=\"line2d_4\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"263.302188\" xlink:href=\"#mc5b05b3048\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_4\">\r\n      <!-- 2 -->\r\n      <g transform=\"translate(260.120938 239.238437)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"xtick_5\">\r\n     <g id=\"line2d_5\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"330.262188\" xlink:href=\"#mc5b05b3048\" y=\"224.64\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_5\">\r\n      <!-- 4 -->\r\n      <g transform=\"translate(327.080938 239.238437)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n   </g>\r\n   <g id=\"matplotlib.axis_2\">\r\n    <g id=\"ytick_1\">\r\n     <g id=\"line2d_6\">\r\n      <defs>\r\n       <path d=\"M 0 0 \r\nL -3.5 0 \r\n\" id=\"m5155e45d6c\" style=\"stroke:#000000;stroke-width:0.8;\"/>\r\n      </defs>\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m5155e45d6c\" y=\"202.896\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_6\">\r\n      <!-- −4 -->\r\n      <g transform=\"translate(7.2 206.695219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_2\">\r\n     <g id=\"line2d_7\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m5155e45d6c\" y=\"159.408\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_7\">\r\n      <!-- −2 -->\r\n      <g transform=\"translate(7.2 163.207219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-8722\"/>\r\n       <use x=\"83.789062\" xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_3\">\r\n     <g id=\"line2d_8\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m5155e45d6c\" y=\"115.92\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_8\">\r\n      <!-- 0 -->\r\n      <g transform=\"translate(15.579688 119.719219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-48\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_4\">\r\n     <g id=\"line2d_9\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m5155e45d6c\" y=\"72.432\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_9\">\r\n      <!-- 2 -->\r\n      <g transform=\"translate(15.579688 76.231219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-50\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n    <g id=\"ytick_5\">\r\n     <g id=\"line2d_10\">\r\n      <g>\r\n       <use style=\"stroke:#000000;stroke-width:0.8;\" x=\"28.942188\" xlink:href=\"#m5155e45d6c\" y=\"28.944\"/>\r\n      </g>\r\n     </g>\r\n     <g id=\"text_10\">\r\n      <!-- 4 -->\r\n      <g transform=\"translate(15.579688 32.743219)scale(0.1 -0.1)\">\r\n       <use xlink:href=\"#DejaVuSans-52\"/>\r\n      </g>\r\n     </g>\r\n    </g>\r\n   </g>\r\n   <g id=\"patch_3\">\r\n    <path d=\"M 28.942188 224.64 \r\nL 28.942188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_4\">\r\n    <path d=\"M 363.742188 224.64 \r\nL 363.742188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_5\">\r\n    <path d=\"M 28.942187 224.64 \r\nL 363.742188 224.64 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n   <g id=\"patch_6\">\r\n    <path d=\"M 28.942187 7.2 \r\nL 363.742188 7.2 \r\n\" style=\"fill:none;stroke:#000000;stroke-linecap:square;stroke-linejoin:miter;stroke-width:0.8;\"/>\r\n   </g>\r\n  </g>\r\n </g>\r\n <defs>\r\n  <clipPath id=\"p0e6de47c32\">\r\n   <rect height=\"217.44\" width=\"334.8\" x=\"28.942188\" y=\"7.2\"/>\r\n  </clipPath>\r\n </defs>\r\n</svg>\r\n",
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAXIAAAD4CAYAAADxeG0DAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8vihELAAAACXBIWXMAAAsTAAALEwEAmpwYAAASj0lEQVR4nO3debRVdd2A8ecrg5hggEwqk6W5NEVZ3iyH0JxSVFgOrTJJTQwtnM0BqMwhjcjhTSEicM70XQ4lIC+IvZpKDogYTiH5OmCoOOWAiXB/7x8bLwoXuHAPd9/fvc9nLdbae5+z9vmusy4Pm3322TdSSkiS8rVB2QNIkurHkEtS5gy5JGXOkEtS5gy5JGWuZRkv2qlTp9S7d+8yXlqSsvXYY4+9kVLqvOL2UkLeu3dvZs6cWcZLS1K2IuLF2rZ7akWSMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMmfIJSlzhlySMlexkEdEi4h4PCImVWqfkqQ1q+QR+anAMxXcnySpDioS8ojoDhwEjK/E/iRJdVepI/IrgLOB6lU9ISKGRMTMiJi5cOHCCr2spKZmafVSHnzpQUbcM4Kp86aWPU4W6h3yiDgYeD2l9NjqnpdSGpdSqkopVXXu3Lm+LyupCXnrw7e4ac5NHHX7UXT5dRf2uGYPXv/gdfb/4v5lj5aFlhXYx+7AgIjoD7QBNomIG1NKgyqwb0lNUEqJOa/PYfLcyUx+bjJ/m/83qtPy/9DvveXejDloDBFR4pT5qHfIU0rDgGEAEbEX8GMjLqk2M16ewfVPXM/k5yYz/935tT5nm0234dZv3UqrFq0aeLp8eR25pAazfZftade6Ha++/2qtj3fcqCOTvjuJDht1aODJ8lbRkKeU7k0pHVzJfUpqOjbZcBNO/urJ7LzZzis91mqDVtzx7TvYquNWJUyWN4/IJTWI6lTNmEfH8OUxX+bhVx5e6fHxA8bTr1e/EibLnyGXtN7NfXMue127F0PvGsr7i98HYFCfQbTcoPiYbvgewzl6x6PLHDFrlbhqRZJqtaR6CZfOuJTz7j2Pj5Z+BECPTXrwu4N/x4FbH8gDLz1A1eZVXLj3hSVPmjdDLmm9mP3qbAbfOZhZC2bVbBv6laFcss8ltNuwHQBHbHsE53/jfDYITw7UhyGXVFH/WfIfLrzvQkY+OJKlaSkAW3fcmgkDJvD1Xl//zHNH7jfSiFeAIZdUMTNensHgOwfz7BvPAtAiWnDWbmfxsz1/xkatNlrp+Ua8Mgy5pHp7f/H7DL9nOFc9chWJBMCOXXdkwoAJ7Lz5ypcaqrIMuaR6mfbPaQyZOIQX//0iAK1btOa8Pc/jrN3O8tuZDcSQS1onb334FmdOO5NrZ19bs223Hrsx/pDxbNt52/IGa4YMuaS1dtvTtzH0rqG89sFrAGzcamMu2ecShu4y1PPeJTDkkurs1fdf5aS7TuK2Z26r2bbfF/Zj3CHj6N2+d3mDNXOGXNIapZS47onrOGPqGbz9n7cBaN+mPZd/83KO2fEYbzdbMkMuabVeeOcFTph0AtP+Oa1m22HbHsbo/qPp1rZbiZPpE4ZcUq2qUzWjHxnNsHuG8cHHHwDQdeOujO4/msO3O7zk6fRphlzSSp5Z+AzHTzyeGS/PqNl27E7Hcun+l9Jxo44lTqbaGHJJNT5e+jGjZozi/PvOZ/HSxQD0+nwvxh0yzt+f2YgZckkAzFowi8F3Dmb2q7MBCIKTdjmJi/e5mLat25Y7nFbLkEvN3Icff8gF913AqBmjam5ytc2m2zBhwAR277l7ydOpLgy51Izd/+L9HD/xeOa+ORcobnJ1zu7n8NM9f0qblm1Knk51ZcilZui9j97j3OnnMmbmmJptfbv15eqBV7NTt53KG0zrxJBLzcyU56ZwwqQTePndlwHYsMWGnL/X+Zyx6xne5CpThlxqJt5c9CanTz2dG/5+Q822PXruwfhDxrNNp21KnEz1ZcilJi6lxK1P38pJU07i9Q9eB6Bt67aM3HckJ1ad6E2umgBDLjVh/3rvXwy9ayh/evZPNdsO2OoAxh40ll7te5U3mCrKkEtNUEqJqx+/mjOnncm/P/o3AB036sgV37yCQX0GeZOrJsaQS03M828/z5CJQ7jn/+6p2fat7b7FlQdeSde2XUucTOuLIZeaiKXVS7nykSsZ8ZcRLPp4EQDd2nZjTP8xHLrtoSVPp/XJkEtNwNMLn2bwnYN5aP5DNdsG9x3MqP1G0WGjDiVOpoZgyKWMLV66mJEPjOSi+y+quclV7/a9+f0hv2ffL+xb8nRqKIZcytSjrzzK4DsHM+f1OUBxk6tTv3oqF+19ERu33rjk6dSQDLmUmUUfL+Ln9/6cS/92KdWpGoBtO23LhAET2LXHriVPpzIYcikj971wH8dPPJ55b80DoOUGLRm2xzBGfH0EG7bcsOTpVBZDLmXg3Y/e5Zy7z2HsY2Nrtu282c5cPfBq+nTtU+JkagwMudTITZ47mRMnn8j8d+cD0KZlGy7Y6wJO3/V0Wm7gX2FVIOQR0QO4HugKJGBcSum/6rtfqblb+MFCTpt6GjfNualmW79e/Rh/yHi23nTrEidTY1OJf86XAGemlGZFRDvgsYi4O6X0dAX2LTU7KSVueeoWTp5yMm8segOAdq3b8av9fsWQnYd4kyutpN4hTyktABYsW34vIp4BtgAMubQOTvuf0/jNI7+pWe+/dX/GHjSWHp/vUeJUaswq+k97RPQG+gIPV3K/UnNy+GZ7A7DpRpty46E3MunISUZcq1WxT0oioi1wG3BaSundWh4fAgwB6NmzZ6VeVmo6qqvhssvolxLXDLyG/lv3p8vGXcqeShmIlFL9dxLRCpgETE0pXbam51dVVaWZM2fW+3WlJmPBAjj6aLjnHnjpJejeveyJ1AhFxGMppaoVt9f71EoUNzaeADxTl4hLWsHEidCnD0yfDvvvb8S11ipxjnx34HvA3hExe9mf/hXYr9S0ffghDB0KAwbAG8XVKRx3XLkzKUuVuGrlAcBfNyKtjTlz4Mgj4amnlm/r0KGIurSWvCBVakgpwVVXwVe+8tmIAxx1FLRpU85cyprf75UaysKF8P3vw+TJtT/uaRWtI4/IpYYyb15xJL7ffis/tuOO0Ldvw8+kJsGQSw1l113hvPNqvyrFo3HVgyGXGtKECXDNNcXy175WfMDZunVxflxaR54jlxrK448XlxsCdO4Mt94K48fDk0/CppuWO5uyZsilhvDOO3DEEfDRR7DBBvDHP8IWW8AppxSXIkr14KkVaX2rroZjjoHnny/WL7gA9tmnWO7QAfr1K282NQmGXFrfRo2CO+8slg86CIYNK3ceNTmGXFqf7r0Xhg8vlnv3huuvL06tSBXkT5S0vixYAN/5TnFqpXXr4sPNjh3LnkpNkCGX1oePP4Zvfxtee61Yv/JK2HnncmdSk2XIpfVh+HC4//5i+eij4Qc/KHceNWmGXKq022+HX/+6WN5hB/jtbyG8QajWH0MuVdJzzxU3xgJo1644L/65z5U7k5o8Qy5VyqJFcPjh8O6yX1l77bXwpS+VOpKaB0MuVUJK8KMfLf+W5hlnwGGHlTuTmg1DLlXC+PFw3XXF8h57wC9/We48alYMuVRfs2bByScXy126wC23QKtW5c6kZsWQS/Xx9tvFefFPboZ1882w+eZlT6VmxpBL66q6urhG/IUXivVf/AK+8Y1SR1LzZMildTVyJEyaVCwfcgicfXa586jZMuTSuvjLX+AnPymWt9yy+KDTm2GpJP7kSWvrlVeW3wxrww3httuK+4pLJTHk0tr45GZYCxcW61ddBX37ljuTmj1DLq2Nc86BBx8slo89FgYPLnUcCQy5VHe33gqXX14s9+kDo0d7Myw1CoZcqou5c+G444rlTTYpzot7Myw1EoZcWpMPPii+9PPee8X6tdfCVluVOpL0aYZcWp2U4Ic/hCefLNbPOgsOPbTcmaQVGHJpdcaNgxtuKJb79YOLLy53HqkWhlxalZkz4ZRTiuWuXYv7qLRsWe5MUi0MuVSbt96CI46AxYuhRYvijoabbVb2VFKtDLm0oupqGDQIXnyxWL/4Ythzz3JnklbDkEsruvhimDKlWB44sPiAU2rEKhLyiDggIv4REfMi4txK7FMqxfTp8LOfFctf/GJxqaFf+lEjV++QR0QLYDRwILAdcGREbFff/UoNbv58OPLI4pLDNm2Kb3K2b1/2VNIaVeKIfBdgXkrp+ZTSYuBmYGAF9is1rIcfhnfeKZZHj4addipzGqnOKnEt1RbAy59anw98dcUnRcQQYAhAz549K/CyUoUdfjj89a8wceLyr+NLGWiwi2JTSuOAcQBVVVWpoV5XWiu77lr8kTJSiVMrrwA9PrXefdk2SVIDqETIHwW2jogtI6I18B3gzgrsV5JUB/U+tZJSWhIRJwFTgRbA1Smlp+o9mSSpTipyjjyldBdwVyX2JUlaO36zU5IyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXOGXJIyZ8glKXP1CnlEjIqIZyPi7xFxR0S0r9BckqQ6qu8R+d3A9imlPsBcYFj9R5IkrY16hTylNC2ltGTZ6kNA9/qPJElaG5U8R34cMKWC+5Mk1UHLNT0hIqYD3Wp5aERK6c/LnjMCWAL8YTX7GQIMAejZs+c6DStJWtkaQ55S2nd1j0fEscDBwD4ppbSa/YwDxgFUVVWt8nmSpLWzxpCvTkQcAJwN7JlSWlSZkSRJa6O+58ivAtoBd0fE7IgYW4GZJElroV5H5CmlrSo1iCRp3fjNTknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKnCGXpMwZcknKXEVCHhFnRkSKiE6V2J8kqe7qHfKI6AHsD7xU/3EkSWurEkfklwNnA6kC+5IkraV6hTwiBgKvpJSeqMNzh0TEzIiYuXDhwvq8rCTpU1qu6QkRMR3oVstDI4DhFKdV1iilNA4YB1BVVeXRuyRVyBpDnlLat7btEbEDsCXwREQAdAdmRcQuKaVXKzqlJGmV1hjyVUkpzQG6fLIeES8AVSmlNyowlySpjryOXJIyt85H5CtKKfWu1L4kSXXnEbkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmDLkkZc6QS1LmIqWG/z3IEbEQeLHBX/izOgH+WrqC78VyvhfL+V4s11jei14ppc4rbiwl5I1BRMxMKVWVPUdj4HuxnO/Fcr4XyzX298JTK5KUOUMuSZlrziEfV/YAjYjvxXK+F8v5XizXqN+LZnuOXJKaiuZ8RC5JTYIhl6TMGXIgIs6MiBQRncqepSwRMSoino2Iv0fEHRHRvuyZGlpEHBAR/4iIeRFxbtnzlCUiekTE/0bE0xHxVEScWvZMZYuIFhHxeERMKnuW2jT7kEdED2B/4KWyZynZ3cD2KaU+wFxgWMnzNKiIaAGMBg4EtgOOjIjtyp2qNEuAM1NK2wFfA4Y24/fiE6cCz5Q9xKo0+5ADlwNnA836U9+U0rSU0pJlqw8B3cucpwS7APNSSs+nlBYDNwMDS56pFCmlBSmlWcuW36MI2BblTlWeiOgOHASML3uWVWnWIY+IgcArKaUnyp6lkTkOmFL2EA1sC+DlT63PpxnH6xMR0RvoCzxc8ihluoLiYK+65DlWqWXZA6xvETEd6FbLQyOA4RSnVZqF1b0XKaU/L3vOCIr/Wv+hIWdT4xMRbYHbgNNSSu+WPU8ZIuJg4PWU0mMRsVfJ46xSkw95Smnf2rZHxA7AlsATEQHFqYRZEbFLSunVBhyxwazqvfhERBwLHAzsk5rfFwxeAXp8ar37sm3NUkS0ooj4H1JKt5c9T4l2BwZERH+gDbBJRNyYUhpU8lyf4ReClomIF4CqlFJjuMNZg4uIA4DLgD1TSgvLnqehRURLig9596EI+KPAd1NKT5U6WAmiOLK5DngrpXRayeM0GsuOyH+cUjq45FFW0qzPkeszrgLaAXdHxOyIGFv2QA1p2Qe9JwFTKT7c++/mGPFldge+B+y97Gdh9rIjUjVSHpFLUuY8IpekzBlyScqcIZekzBlyScqcIZekzBlyScqcIZekzP0/+X1zHHVZzdgAAAAASUVORK5CYII=\n"
     },
     "metadata": {
      "needs_background": "light"
     }
    }
   ],
   "source": [
    "plt.quiver([0, v[0]], [0, v[1]], [v[0], w[0]], [v[1], v[1]], angles='xy', scale_units='xy', scale=1, color= ['r', 'g'])\n",
    "plt.xlim(-5, 5)\n",
    "plt.ylim(-5, 5)\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ]
}