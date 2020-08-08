# Pokemon Classifier based on [fast.ai](https://www.fast.ai) library deployed on Heroku.

This repo can be used as a starting point to deploy [fast.ai](https://github.com/fastai/fastai) models on Render.

The sample app described here is up at https://pokemonclassifierapp.herokuapp.com/. Test it out with pikachu,charmander or bulbasaur images!

You can check the notebook [here.](https://gist.github.com/sachinchaturvedi93/33428a6fcc80ae6e75da81078d36fbd3)

## Notes

1. The starter codes is taken from the starter code for deploying [fast.ai](https://www.fast.ai) models on [Render](https://github.com/render-examples/fastai-v3).

2. We need to add a Procfile to the repository and put `web: python app/server.py serve` in it.

3. We need to add a runtime.txt file to specify `python` version.

4. In the `server.py` file we need to add : 
``` 
import os 
import requests
Port = int(os.environ.get('PORT', 50000))
```
and replace uvicorn.run(.....) by
```
uvicorn.run(app=app, host='0.0.0.0', port=Port, log_level="info")
```
Edit : After upgrading uvicorn version, the app crashed with the following error - 
[Publish to Heroku is broken: "WARNING: You must pass the application as an import string to enable 'reload' or 'workers"](https://github.com/simonw/datasette/issues/633)

Solution is changing WEB_CONCURRENCY = 1 in app's setting on Heroku dashboard.
