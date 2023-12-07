## android-samples
# Save Screenshot

Select any view (LinearLayout, CardView) and pass it to the 'getScreenshot' function; that area will be captured.
```java
  public Bitmap getScreenShot(View view) {
        View screenView = view;//.getRootView();
        screenView.setDrawingCacheEnabled(true);
        Bitmap bitmap = Bitmap.createBitmap(screenView.getDrawingCache());
        screenView.setDrawingCacheEnabled(false);
        return bitmap;
    }
```
1) The captured screenshot will be saved inside the "Screenshots" directory.

```java
    public void store(Bitmap bm, String fileName){
        File directory = new File(Environment.getExternalStorageDirectory(), "Pictures/Screenshots");

        if(!directory.exists())
            directory.mkdirs();

        File file = new File(directory, fileName + ".png");
        try {
            FileOutputStream fOut = new FileOutputStream(file);
            bm.compress(Bitmap.CompressFormat.PNG, 85, fOut);
            fOut.flush();
            fOut.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```

```java
String fileName ="Screenshot";//any given name
layout = findViewById(R.id.layout);
store(getScreenShot(layout),fileName+".jpg");
```
2) The captured screenshot will be saved inside the "Azhar" directory.

Directory 'Azhar'  will be created in Pictures and bitmap( from getScreenShot funtion)  with filename passed to function
```java
    public void store(Bitmap bm, String fileName){
        File directory = new File(Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES) ;
        File picturesDirectory = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES);
        File azharDirectory = new File(picturesDirectory, "Azhar");
        if(!azharDirectory.exists())
            azharDirectory.mkdirs();

        File file = new File(azharDirectory, fileName + ".png");
        try {
            FileOutputStream fOut = new FileOutputStream(file);
            bm.compress(Bitmap.CompressFormat.PNG, 85, fOut);
            fOut.flush();
            fOut.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```

```java
String fileName ="Screenshot";//any given name
layout = findViewById(R.id.layout);
store(getScreenShot(layout),fileName+".jpg");
```