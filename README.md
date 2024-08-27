# idx-ctv-andorid-sdk

This guide provides detailed instructions on how to integrate and use the IDX CTV SDK in your Android project.

## Installation

Incorporate the Data Manager Provider SDK into your project by adding the following line to the `dependencies` section of your `app/build.gradle` file:

```gradle
implementation 'com.dxmdp.android:ctv:0.0.1'
```

## Initialization DataManagerProvider

The SDK requires initialization with a valid `providerId` from the IDX before usage.

Start by importing the necessary classes:

```java
import com.dxmdp.android.ctv.DMPCtv;
import com.dxmdp.android.ctv.requests.event.EventRequestProperties;
```

Then, initialize the SDK within the `onCreate` method of your `MainActivity` class:

```java
public class MainActivity extends AppCompatActivity {
  private DMPAdBuilder dmpAdBuilder;

  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    String providerId = "Your Provider ID goes here";
    dmpCtv = new DMPCtv(
        getApplicationContext(),
        providerId,
        "My example app",
        "1.0.0"
    );
  }
}
```

> **Note:** Replace `"Your Provider ID goes here"` with your actual `providerId` obtained from IDX representative.

## Usage

### Tracking Pageview Events

Here's an example of tracking pageview events within the `onResume` method of an Activity:

```java
@Override
protected void onResume() {
    super.onResume();

    EventRequestProperties eventRequestProperties = new EventRequestProperties();

    // Set the relevant properties
    eventRequestProperties.setUrl("/examplePage"); // Replace with the specific page URL or identifier
    eventRequestProperties.setTitle("Example Page Title"); // Replace with the specific page title
    eventRequestProperties.setDomain("your-domain.com"); // Replace with your domain
    eventRequestProperties.setAuthor("author"); // Replace with the author of the page
    eventRequestProperties.setCategory("category"); // Replace with the category of the page
    eventRequestProperties.setDescription("This is an example page."); // Replace with the description of the page
    eventRequestProperties.setTags(Arrays.asList("tag1", "tag2", "tag3")); // Replace with the tags related to the page

    // Send the event
    dmpCtv.sendPageViewEvent(eventRequestProperties).thenRun(() -> {
        System.out.println("CTV EVENTS: " + dmpCtv.getDefinitionIdsAsString());
    });
}
```

## Support

For support, report issues in the issue tracker or reach out through our designated support channels.

## License

The IDX CTV SDK is licensed under the MIT License.

```
MIT License
Copyright (c) 2024 IDX LTD

Permission is granted to freely use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of this software, subject to including the above copyright notice and this permission notice in all copies or substantial portions of the Software.

The software is provided "AS IS", without warranty of any kind. Refer to the [LICENSE](LICENSE) file for full details.