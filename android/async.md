# What is an AsyncTask?

AsyncTask is an abstract Android class which helps the Android applications to handle the Main UI thread in efficient way. AsyncTask class allows us to perform long lasting tasks/background operations and show the result on the UI thread without affecting the main thread.


AsyncTask is a wrapper class that encloses the functionality of Thread.


This class allows you to perform background operations and publish results on the UI thread without having to manipulate threads and/or handlers.


The AsyncTask must be called from the UI thread. Task can only happen once. Error will be thrown if more than once.


# Provide an example of one?

```
private class GetWeatherTask extends AsyncTask<String, Void, String> {
    private TextView textView;

    public GetWeatherTask(TextView textView) {
        this.textView = textView;
    }

    @Override
    protected String doInBackground(String... strings) {
        String weather = "UNDEFINED";
        try {
            URL url = new URL(strings[0]);
            HttpURLConnection urlConnection = (HttpURLConnection) url.openConnection();

            InputStream stream = new BufferedInputStream(urlConnection.getInputStream());
            BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(stream));
            StringBuilder builder = new StringBuilder();

            String inputString;
            while ((inputString = bufferedReader.readLine()) != null) {
                builder.append(inputString);
            }

            JSONObject topLevel = new JSONObject(builder.toString());
            JSONObject main = topLevel.getJSONObject("main");
            weather = String.valueOf(main.getDouble("temp"));

            urlConnection.disconnect();
        } catch (IOException | JSONException e) {
            e.printStackTrace();
        }
        return weather;
    }

    @Override
    protected void onPostExecute(String temp) {
        textView.setText("Current Weather: " + temp);
    }
}
```

And executing it from onCreate (but you shouldn't):

```
TextView textView = (TextView) findViewById(R.id.textView);
new GetWeatherTask(textView).execute(url);
```


# What are the four steps?

- onPreExecute
- doInBackground
- onProgressUpdate
- onPostExecute

# How do you cancel an AsyncTask?

```
myTask.cancel(true);
```


# What's the relationship between an Async and Activity?

They aren't related. So if you start an AsyncTask in an activity, rotate the device. On the completion of the AsyncTask, it will have the wrong view b/c it was from onCreate pre rotation. This can cause an exception and memory leak.


Source:
- https://www.quora.com/What-is-AsyncTask-in-Android
- https://stackoverflow.com/questions/26156269/executing-a-thread-in-asynctask-and-its-complications
- https://stackoverflow.com/questions/6039158/android-cancel-async-task
- https://www.mindstick.com/forum/33396/what-is-the-relationship-between-the-life-cycle-of-an-asynctask-and-an-activity
