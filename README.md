# Guess The Word
- A game of charades.
- Made with Google Code Labs!
- MVVM
- LiveData
- Databinding
- String Formatting

## This app uses Android Architecture Components
 - UI Controller: 
 A UI controller is a UI-based class such as Activity or Fragment. A UI controller should only contain logic that handles UI and operating-system interactions such as displaying views and capturing user input. Don't put decision-making logic, such as logic that determines the text to display, into the UI controller.

 - ViewModel:
 A ViewModel holds data to be displayed in a fragment or activity associated with the ViewModel. A ViewModel can do simple calculations and transformations on data to prepare the data to be displayed by the UI controller. In this architecture, the ViewModel performs the decision-making.

 - ViewModel Factory:
 A viewModel Factory instantiates ViewModel objects, with or without constructor parameters. A factory method is a method that returns an instance of the same class.

 - LiveData:
 LiveData lets you build data objects that notify views when the underlying database changes. To use the LiveData class, you set up "observers" (for example, activities or fragments) that observe changes in the app's data. LiveData is lifecycle-aware, so it only updates app-component observers that are in an active lifecycle state. LiveData is observable, which means that an observer is notified when the data held by the LiveData object changes. LiveData holds data; LiveData is a wrapper that can be used with any data. LiveData is lifecycle-aware. When you attach an observer to the LiveData, the observer is associated with a LifecycleOwner (usually an Activity or Fragment). Usually, LiveData delivers updates to the observers only when data changes. An exception to this behavior is that observers also receive updates when the 
 observer changes from an inactive to an active state.

 - Transformations.map()
 The Transformations.map() method provides a way to perform data manipulations on the source LiveData and return a result LiveData object. These transformations aren't calculated unless an observer is observing the returned LiveData object. This method takes the source LiveData and a function as parameters. The function manipulates the source LiveData. The lambda function passed to Transformation.map() is executed on the main thread, so do not include long-running tasks.

 - Formatting Dates
 The DateUtils.formatElapsedTime() utility method takes a long number of milliseconds and formats the number to use a MM:SS string format.


 #### Why use viewLifecycleOwner?
Fragment views get destroyed when a user navigates away from a fragment, even though the fragment itself is not destroyed. This essentially creates two lifecycles, the lifecycle of the fragment, and the lifecycle of the fragment's view. Referring to the fragment's lifecycle instead of the fragment view's lifecycle can cause subtle bugs when updating the fragment's view. Therefore, when setting up observers that affect the fragment's view you should:

1. Set up the observers in onCreateView()

2. Pass in viewLifecycleOwner to observers

#### Encapsulation
Encapsulation is a way to restrict direct access to some of an object's fields. When you encapsulate an object, you expose a set of public methods that modify the private internal fields. Using encapsulation, you control how other classes manipulate these internal fields. Only the ViewModel should edit the data in your app. But UI controllers need to read the data, so the data fields can't be completely private. To encapsulate your app's data, you use both MutableLiveData and LiveData objects.

- MutableLiveData vs. LiveData:
Data in a MutableLiveData object can be changed, as the name implies. Inside the ViewModel, the data should be editable, so it uses MutableLiveData.
Data in a LiveData object can be read, but not changed. From outside the ViewModel, data should be readable, but not editable, so the data should be exposed as LiveData. To carry out this strategy, you use a Kotlin backing property. A backing property allows you to return something from a getter other than the exact object.

#### The observer pattern
The observer pattern is a software design pattern. It specifies communication between objects: an observable (the "subject" of observation) and observers. An observable is an object that notifies observers about the changes in its state. In the case of LiveData in this app, the observable (subject) is the LiveData object, and the observers are the methods in the UI controllers, such as fragments. A state change happens whenever the data wrapped inside LiveData changes. The LiveData classes are crucial in communicating from the ViewModel to the fragment.

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
