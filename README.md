# Guess The Word
- A game of charades.
- Made with Google Code Labs
- Uses MVVM

## This app uses Android Architecture Components
 - UI Controller: 
 A UI controller is a UI-based class such as Activity or Fragment. A UI controller should only contain logic that handles UI and operating-system interactions such as displaying views and capturing user input. Don't put decision-making logic, such as logic that determines the text to display, into the UI controller.

 - ViewModel:
 A ViewModel holds data to be displayed in a fragment or activity associated with the ViewModel. A ViewModel can do simple calculations and transformations on data to prepare the data to be displayed by the UI controller. In this architecture, the ViewModel performs the decision-making.

 - ViewModel Factory
 A viewModel Factory instantiates ViewModel objects, with or without constructor parameters. A factory method is a method that returns an instance of the same class.


### UI controller
- An example of a UI controller is the ScoreFragment that you created in this codelab.
- Doesn't contain any data to be displayed in the UI.
- Contains code for displaying data, and user-event code such as click listeners.
- Destroyed and re-created during every configuration change.
- Contains views.
- Contains a reference to the associated ViewModel.

### ViewModel
- An example of a ViewModel is the ScoreViewModel that you created in this codelab.
- Contains data that the UI controller displays in the UI.
- Contains code for data processing.
- Destroyed only when the associated UI controller goes away permanently—for an activity, when the activity finishes, or for a fragment, when the fragment is detached.
- Should never contain references to activities, fragments, or views, because they don't survive configuration changes, but the ViewModel does.
- Doesn't contain any reference to the associated UI controller.
