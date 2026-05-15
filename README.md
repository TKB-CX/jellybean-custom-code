# Files

| File | Notes |
|---|---|
| custom_code.html | This is saved in the overall settings of the Webflow site and controls what page the user sees based on whether a correct guess has been made or not. It also parses people guesses to either set the game as won or redirect to try again. |
| home.html | Goes into the settings for the Home page and ensures people can only access this page if the correct guess hasn't been made |
| tryagain.html | Goes into the settings for the Try Again page and shows the try again message that's been randomly selected |
| winner.html | Prevents direct access to this page and redirects the user to the correct page based on whether the correct guess has been made or not |

Where the below code exists in the areas above:

```
if (window.location.hostname === 'jellybeans.webflow.io') {
  	docName = 'staging-status';
}
```

`jellybeans.webflow.io` needs to be updated to the Webflow custom URL of the project you're editing

# Making Changes to Webflow Project

Due to the way this page needed to be put together there's some things to keep in mind when editing the pages:

* To be able to see the content of the home page behind the explosion gif, you need to click into the Overlay block, go to Layout in the Style tab and set it to None. Remember to switch it back to Block once you've finished editing the slide content before publishing
* The content of the home page is in a Slider, by default you're shown the first slide. To see subsequent slides, select them in the Navigator on the left hand side, then on the right hand panel select Settings, this should bring the selected Slide into view.
* On the Winner page there's a form for the winner to enter their details, you may want to change the Success Message of that form. To view that message select the Form Block element in the left hand Navigator panel. Then go to Settings in the right hand panel, scroll down to "Form Block settings" and select Success Message

# Firestore Database

The correct answer is stored in a Firestore database within the cxteam@thinkerbell.com Firebase, the project is called Jellybeans

* There's one collection with 2 documents, status and staging-status, they both operate the same way with the same values but when you're testing with the Webflow generated URL it will be read/writing to staging-status (as long as you've made the URL changes outlined at the beginning of this doc)
* The base fields required in these are:
* * correctAnswer - set this to the value you're trying to get them to guess
* * isWon - should be false by default, changes to `true` when the game is won
* The extra fields created when someone wins:
* * winnerGuess - the correct value will be stored here
* * winnerToken - A randomly generated token will be saved here, this ensures the winner is then shown the Winner page instead of the Game Over page
* To reset the game, delete the winnerGuess and winnerToken fields and switch isWon back to false from `true`