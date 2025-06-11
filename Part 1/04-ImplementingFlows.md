## Implementing Flows


<b>Aim : </b> Generate a random movie genre and suggest a popular movie.


```python
# !pip install crewai
# !pip install crewai-tools
```


```python
from dotenv import load_dotenv
load_dotenv()

from crewai import Agent, Task, Crew
from crewai.flow.flow import Flow, start, listen

import openai
import os

openai_client = openai.OpenAI(api_key = os.getenv("OPENAI_API_KEY"))
```


```python
class MovieRecommendationFlow(Flow):
    
    @start()
    def generate_genre(self):
        response = openai_client.chat.completions.create(
            model = "gpt-4o-mini",
            messages = [
                {
                    "role" : "user",
                    "content" : "Give me a random movie genre."
                }
            ]
        )

        random_genre = response.choices[0].message.content.strip()
        self.state['genre'] = random_genre
        return random_genre
    

    @listen(generate_genre)
    def recomment_movie(self, random_genre):
        response = openai_client.chat.completions.create(
            model = "gpt-4o-mini",
            messages = [
                {
                    "role" : "user",
                    "content" : f"Recommend a movie in the genre of {random_genre}."
                }
            ]
        )

        movie_recommendation = response.choices[0].message.content.strip()
        self.state['recommendation'] = movie_recommendation
        return movie_recommendation
```


```python
flow = MovieRecommendationFlow()

final_result = await flow.kickoff_async()

print(final_result)
```

    [34m╭─[0m[34m──────────────────────────────[0m[34m Flow Execution [0m[34m──────────────────────────────[0m[34m─╮[0m
    [34m│[0m                                                                              [34m│[0m
    [34m│[0m  [1;34mStarting Flow Execution[0m                                                     [34m│[0m
    [34m│[0m  [37mName: [0m[34mMovieRecommendationFlow[0m                                               [34m│[0m
    [34m│[0m  [37mID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m                                    [34m│[0m
    [34m│[0m                                                                              [34m│[0m
    [34m│[0m                                                                              [34m│[0m
    [34m╰──────────────────────────────────────────────────────────────────────────────╯[0m
    
    [1;34m🌊 Flow: [0m[34mMovieRecommendationFlow[0m
    [37m    ID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m
    └── [33m🧠 Starting Flow...[0m
    
    [1m[35m Flow started with ID: bf267161-9a56-4aed-9ead-c1175878d02c[00m
    [1;34m🌊 Flow: [0m[34mMovieRecommendationFlow[0m
    [37m    ID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m
    ├── [33m🧠 Starting Flow...[0m
    └── [1;33m🔄 Running:[0m[1;33m generate_genre[0m
    
    [1;34m🌊 Flow: [0m[34mMovieRecommendationFlow[0m
    [37m    ID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m
    ├── [37mFlow Method Step[0m
    └── [1;32m✅ Completed:[0m[1;32m generate_genre[0m
    
    [1;34m🌊 Flow: [0m[34mMovieRecommendationFlow[0m
    [37m    ID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m
    ├── [37mFlow Method Step[0m
    ├── [1;32m✅ Completed:[0m[1;32m generate_genre[0m
    └── [1;33m🔄 Running:[0m[1;33m recomment_movie[0m
    
    [1;34m🌊 Flow: [0m[34mMovieRecommendationFlow[0m
    [37m    ID: [0m[34mbf267161-9a56-4aed-9ead-c1175878d02c[0m
    ├── [37mFlow Method Step[0m
    ├── [1;32m✅ Completed:[0m[1;32m generate_genre[0m
    └── [1;32m✅ Completed:[0m[1;32m recomment_movie[0m
    
    [1;32m✅ Flow Finished: [0m[32mMovieRecommendationFlow[0m
    ├── [37mFlow Method Step[0m
    ├── [1;32m✅ Completed:[0m[1;32m generate_genre[0m
    └── [1;32m✅ Completed:[0m[1;32m recomment_movie[0m
    [32m╭─[0m[32m─────────────────────────────[0m[32m Flow Completion [0m[32m──────────────────────────────[0m[32m─╮[0m
    [32m│[0m                                                                              [32m│[0m
    [32m│[0m  [1;32mFlow Execution Completed[0m                                                    [32m│[0m
    [32m│[0m  [37mName: [0m[32mMovieRecommendationFlow[0m                                               [32m│[0m
    [32m│[0m  [37mID: [0m[32mbf267161-9a56-4aed-9ead-c1175878d02c[0m                                    [32m│[0m
    [32m│[0m                                                                              [32m│[0m
    [32m│[0m                                                                              [32m│[0m
    [32m╰──────────────────────────────────────────────────────────────────────────────╯[0m
    
    A great psychological thriller to watch is "Gone Girl" (2014), directed by David Fincher. The film is based on the novel by Gillian Flynn and follows the story of Nick Dunne, whose wife, Amy, goes missing on their fifth wedding anniversary. As the investigation unfolds, secrets about their marriage and Amy's mysterious past come to light, leading to unexpected twists and a gripping exploration of media perception and deceit. The performances by Ben Affleck and Rosamund Pike are particularly noteworthy, making this film a compelling choice for fans of the genre.



```python
from IPython import display
display.display(display.Markdown(f"{final_result}"))
```


A great psychological thriller to watch is "Gone Girl" (2014), directed by David Fincher. The film is based on the novel by Gillian Flynn and follows the story of Nick Dunne, whose wife, Amy, goes missing on their fifth wedding anniversary. As the investigation unfolds, secrets about their marriage and Amy's mysterious past come to light, leading to unexpected twists and a gripping exploration of media perception and deceit. The performances by Ben Affleck and Rosamund Pike are particularly noteworthy, making this film a compelling choice for fans of the genre.



```python
flow.state
```




    {'id': 'bf267161-9a56-4aed-9ead-c1175878d02c',
     'genre': 'How about "psychological thriller"?',
     'recommendation': 'A great psychological thriller to watch is "Gone Girl" (2014), directed by David Fincher. The film is based on the novel by Gillian Flynn and follows the story of Nick Dunne, whose wife, Amy, goes missing on their fifth wedding anniversary. As the investigation unfolds, secrets about their marriage and Amy\'s mysterious past come to light, leading to unexpected twists and a gripping exploration of media perception and deceit. The performances by Ben Affleck and Rosamund Pike are particularly noteworthy, making this film a compelling choice for fans of the genre.'}


