NYT-Based News Tagger
=====================

A labeller for news articles trained on the [NYT annotated corpus](https://catalog.ldc.upenn.edu/ldc2008t19)
by Jasmin Rubinovitz as part of the [MIT Media Lab SuperGlue project](https://www.media.mit.edu/projects/superglue/overview/).
Give it the clean text of a story (ie. no html content), and it returns various descriptors
and taxonomic classifiers based on models trained on the taging in the NYT corpus.

We use it in the Media Cloud project to automatically tag every news stories with the themes we think they are about.

Installation
------------

This is built with Python 3. 

On OSX I had to install hdf5 first with brew: `brew install hdf5`.

Do this to install all the Python dependencies (see `doc/python-versions.md` for more info).

```shell
pip install -r requirements.txt  
```

You also need the `word2vec` pre-trained Google News corpus and NYTLabels model.  Run `download_models.py` to get them
(600MB).

Lastly, you'll need `punkt` dataset from NLTK data:

```shell
python -m nltk.downloader -d /usr/local/share/nltk_data punkt
```

Usage
-----

Simply do `run.sh`, or `gunicorn app:app -t 900` and then visit `localhost:8000/` to try it out.

Note: this consumes about **5GB of memory** while running, to keep all the models loaded up.

Deploying
---------

This is built to deploy on Heroku/Dokku.  Set the `WORKERS` environment variable to set how many workers gunicorn
starts with.
