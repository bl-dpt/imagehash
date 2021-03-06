ImageHash
===========

A image hashing library written in Python. ImageHash supports:

* average hashing (`aHash`_)
* perception hashing (`pHash`_)
* difference hashing (`dHash`_)
* wavelet hashing (`wHash`_)
* HSV color hash (colorhash)

|Travis|_ |Coveralls|_

Rationale
---------

Image hashes tell whether two images look nearly identical.
This is different from cryptographic hashing algorithms (like md5, sha-1)
where tiny changes in the image give completely different hashes. 
In image fingerprinting, we actually want our similar inputs to have similar output hashes as well.

The image hash algorithms (average, perception, difference, wavelet)
analyse the image structure on luminence (without color information).
The color hash algorithm analyses the color distribution and 
black & gray fractions (without position information).

Requirements
-------------
Based on PIL/Pillow Image, numpy and scipy.fftpack (for pHash)
Easy installation through `pypi`_::

	pip install imagehash

Basic usage
------------
::

	>>> from PIL import Image
	>>> import imagehash
	>>> hash = imagehash.average_hash(Image.open('test.png'))
	>>> print(hash)
	d879f8f89b1bbf
	>>> otherhash = imagehash.average_hash(Image.open('other.bmp'))
	>>> print(otherhash)
	ffff3720200ffff
	>>> print(hash == otherhash)
	False
	>>> print(hash - otherhash)
	36

The demo script **find_similar_images** illustrates how to find similar images in a directory.

Source hosted at github: https://github.com/JohannesBuchner/imagehash

.. _aHash: http://www.hackerfactor.com/blog/index.php?/archives/432-Looks-Like-It.html
.. _pHash: http://www.hackerfactor.com/blog/index.php?/archives/432-Looks-Like-It.html
.. _dHash: http://www.hackerfactor.com/blog/index.php?/archives/529-Kind-of-Like-That.html
.. _wHash: https://fullstackml.com/2016/07/02/wavelet-image-hash-in-python/
.. _pypi: https://pypi.python.org/pypi/ImageHash


Example results
-----------------

To help evaluate how different hashing algorithms behave, below are a few hashes applied
to two datasets. This will let you know what images an algorithm thinks are basically identical.
For understanding hash distances, check out these excellent blog posts:

* https://tech.okcupid.com/evaluating-perceptual-image-hashes-okcupid/
* https://content-blockchain.org/research/testing-different-image-hash-functions/

The first dataset is a **collection of 7441 free icons on github** (see examples/github-urls.txt).
The following pages show groups of images with the same hash (the hashing method sees them as the same).

* `phash hashsize=8 clusters <https://johannesbuchner.github.io/imagehash/art3.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/art9.html>`__)
* `dhash hashsize=8 clusters <https://johannesbuchner.github.io/imagehash/art4.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/art10.html>`__)
* `whash-haar hashsize=8 clusters <https://johannesbuchner.github.io/imagehash/art5.html>`_ (`with z-transform  <https://johannesbuchner.github.io/imagehash/art11.html>`__)
* `whash-db4 hashsize=8 clusters <https://johannesbuchner.github.io/imagehash/art6.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/art12.html>`__)
* `colorhash binbits=3 clusters <https://johannesbuchner.github.io/imagehash/art7.html>`_
* `average_hash hashsize=8 clusters <https://johannesbuchner.github.io/imagehash/art2.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/art8.html>`__)

The second dataset is a **collection of 109259 art pieces** from parismuseescollections.paris.fr/en/recherche/image-libre/.

The following pages show groups of images with the same hash (the hashing method sees them as the same).

* `phash hashsize:8 clusters <https://johannesbuchner.github.io/imagehash/index3.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/index9.html>`__)
* `dhash hashsize:8 clusters <https://johannesbuchner.github.io/imagehash/index4.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/index10.html>`__)
* `whash-haar hashsize:8 clusters <https://johannesbuchner.github.io/imagehash/index5.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/index11.html>`__)
* `whash-db4 hashsize:8 clusters <https://johannesbuchner.github.io/imagehash/index6.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/index12.html>`__)
* `colorhash binbits:3 clusters <https://johannesbuchner.github.io/imagehash/index7.html>`_
* `average_hash hashsize:8 clusters <https://johannesbuchner.github.io/imagehash/index2.html>`_ (`with z-transform <https://johannesbuchner.github.io/imagehash/index8.html>`__)

You may want to adjust the hashsize or require some manhattan distance (hash1 - hash2 < threshold).

Other projects
---------------

* http://blockhash.io/
* https://github.com/acoomans/instagram-filters
* https://pippy360.github.io/transformationInvariantImageSearch/

Contributing
-------------

Pull requests and new features are welcome.

If you encounter a bug or have a question, please open a Github issue. You can also try stackoverflow.

Changelog
----------

* 4.1: add examples and colorhash

* 4.0: Changed binary to hex implementation, because the previous one was broken for various hash sizes. This change breaks compatibility to previously stored hashes; to convert them from the old encoding, use the "old_hex_to_hash" function.

* 3.5: image data handling speed-up

* 3.2: whash now also handles smaller-than-hash images

* 3.0: dhash had a bug: It computed pixel differences vertically, not horizontally.
       I modified it to follow `dHash`_. The old function is available as dhash_vertical.

* 2.0: added whash

* 1.0: initial ahash, dhash, phash implementations.


.. |Travis| image:: https://travis-ci.org/JohannesBuchner/imagehash.svg?branch=master
.. _Travis: https://travis-ci.org/JohannesBuchner/imagehash

.. |Coveralls| image:: https://coveralls.io/repos/github/JohannesBuchner/imagehash/badge.svg
.. _Coveralls: https://coveralls.io/github/JohannesBuchner/imagehash
