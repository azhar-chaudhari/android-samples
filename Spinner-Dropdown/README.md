## android-samples
# Spinner - Dropdown

## 1) Spinner Using array list


### model class SpinnerRow
```java
public class SpinnerRow {
    String id,title;

    public SpinnerRow(String id, String title) {
        this.id = id;
        this.title = title;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }
}
```
### adapter class SpinnerRowAdapter

```java
public class SpinnerRowAdapter extends BaseAdapter {

    Context context;
    ArrayList<SpinnerRow> objects;

    public SpinnerRowAdapter(Context context, ArrayList<SpinnerRow> objects) {
        super();
        this.context = context;
        this.objects = objects;
    }

    @Override
    public int getCount() {
        return objects.size();
    }

    @Override
    public Object getItem(int position) {
        return objects.get(position);
    }

    @Override
    public long getItemId(int position) {
        return 0;
    }

    public View getView(int position, View convertView, ViewGroup parent) {

        SpinnerRow cur_obj = objects.get(position);
        LayoutInflater inflater = ((Activity) context).getLayoutInflater();
        View row = inflater.inflate(R.layout.spinner_layout, parent, false);
        TextView label =  row.findViewById(R.id.title);//position==0
        label.setHintTextColor(Color.GRAY);
        if(cur_obj.getId().equals("0") || cur_obj.getId()=="0")
        {
           label.setText("");
           label.setHint(cur_obj.getTitle());
        }
        else{

        }
        label.setText(cur_obj.getTitle());

        return row;
    }

    @Override
    public View getDropDownView(int position, View convertView, ViewGroup parent) {
        SpinnerRow currentObject = objects.get(position);
        LayoutInflater inflater = ((Activity) context).getLayoutInflater();
        View row = inflater.inflate(R.layout.spinner_layout, parent, false);
        TextView label =  row.findViewById(R.id.title);//position==0

        if(currentObject.getId().equals("0") || currentObject.getId()=="0")
        {
            row.setBackgroundColor(Color.GRAY);
            label.setHintTextColor(Color.WHITE);
            label.setText("");
            label.setHint(currentObject.getTitle());
        }
        else{
            label.setText(currentObject.getTitle());
        }


        return row;
    }
}
```
### spinner_layout.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="#ffffff"
    android:orientation="vertical">

    <TextView
        android:layout_marginTop="10dp"
        android:id="@+id/title"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textColor="#000000"
        android:textSize="14dp"
        android:padding="10dp"/>
</LinearLayout>
```
### Activity for 1
```java
import com.spinner.example.model.SpinnerRow;

    public class RegistrationActivity extends AppCompatActivity{
        Spinner spinGender;
        String genderSelected="0";

        protected void onCreate(Bundle savedInstanceState) {
            setContentView(R.layout.activity_registration);
            spinGender=findViewById(R.id.spinGender);

            spinGender.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
                @Override
                public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                    SpinnerRow gender=(SpinnerRow)parent.getItemAtPosition(position);
                    genderSelected=gender.getId();
                }

                @Override
                public void onNothingSelected(AdapterView<?> parent) {

                }
            });

            getGenders();
            //or
            //getGendersFromArray();
        }
    
        //using direct class objects 
        private void getGenders(){
            ArrayList<SpinnerRow> spinnerRowArrayList=new ArrayList<>();
            spinnerRowArrayList.add(new SpinnerRow("0","Select Gender *"));
            spinnerRowArrayList.add(new SpinnerRow("Male","Male"));
            spinnerRowArrayList.add(new SpinnerRow("Female","Female"));
            SpinnerRowAdapter  spinnerRowAdapter=new SpinnerRowAdapter(RegistrationActivity.this,spinnerRowArrayList);
            spinGender.setAdapter(spinnerRowAdapter);
            spinnerRowAdapter.notifyDataSetChanged();
        }
        //using array
        private void getGendersFromArray(){
            ArrayList<SpinnerRow> spinnerRowArrayList=new ArrayList<>();
            String[] genders = new String[]{"Male", "Female"};
            for (String gender : genders) {
                spinnerRowArrayList.add(new SpinnerRow(gender, gender));
            }
            SpinnerRowAdapter  spinnerRowAdapter=new SpinnerRowAdapter(RegistrationActivity.this,spinnerRowArrayList);
            spinGender.setAdapter(spinnerRowAdapter);
            spinnerRowAdapter.notifyDataSetChanged();
        }

    }
```
## 

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="gender_array">
        <item>Male</item>
        <item>Female</item>
    </string-array>
</resources>
```

### Activity for 2
```java
import com.spinner.example.model.SpinnerRow;

    public class RegistrationActivity extends AppCompatActivity{
        Spinner spinGender;
        String genderSelected="0";

        protected void onCreate(Bundle savedInstanceState) {
            setContentView(R.layout.activity_registration);
            spinGender=findViewById(R.id.spinGender);

            spinGender.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
                @Override
                public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                    SpinnerRow gender=(SpinnerRow)parent.getItemAtPosition(position);
                    genderSelected=gender.getId();
                }

                @Override
                public void onNothingSelected(AdapterView<?> parent) {

                }
            });

             getGenders();
        }
    
        private void getGenders(){
            
            String[] genderArray = getResources().getStringArray(R.array.my_string_array);

            ArrayList<SpinnerRow> spinnerRowArrayList=new ArrayList<>();
             for (String gender : genderArray) {
                spinnerRowArrayList.add(new SpinnerRow(gender, gender));
            }
            SpinnerRowAdapter  spinnerRowAdapter=new SpinnerRowAdapter(RegistrationActivity.this,spinnerRowArrayList);
            spinGender.setAdapter(spinnerRowAdapter);
            spinnerRowAdapter.notifyDataSetChanged();
        }
    }
```


## 3) Using api

### Activity for 3
```java
import com.spinner.example.model.SpinnerRow;
    public class RegistrationActivity extends AppCompatActivity{
        Spinner spinGender;
        String genderSelected="0";

        protected void onCreate(Bundle savedInstanceState) {
            setContentView(R.layout.activity_registration);
            spinGender=findViewById(R.id.spinGender);

            spinGender.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
                @Override
                public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                    SpinnerRow gender=(SpinnerRow)parent.getItemAtPosition(position);
                    genderSelected=gender.getId();
                }

                @Override
                public void onNothingSelected(AdapterView<?> parent) {

                }
            });

            getGenders("http://some-domain/api/get_gender_api");
        }
    

        private void getGenders(String url)  {
            ProgressDialog progressBar = new ProgressDialog(this);
            progressBar.setCancelable(true);
            progressBar.setMessage("Fetching data please wait...");
            progressBar.show();
            OkHttpClient client = new OkHttpClient();
            RequestBody formBody = new FormBody.Builder()
                    .build();
        
            Request request = new Request.Builder()
                    .url(url)
                    .post(formBody)
                    .build();

            client.newCall(request).enqueue(new Callback() {
                @Override
                public void onFailure(Call call, IOException e) {
                    // call.cancel();
                    runOnUiThread(() -> {
                        progressBar.dismiss();
                    });
                }

                @Override
                public void onResponse(Call call, Response response) throws IOException {

                    final String myResponse = response.body().string();
                  
                    runOnUiThread(() -> {
                        progressBar.dismiss();
                    });
                    ArrayList<SpinnerRow> spinnerRowArrayList=new ArrayList<>();
                    spinnerRowArrayList.add(new SpinnerRow("0","Select  Gender"));
                    try {

                        JSONArray jsonArray=new JSONArray(myResponse);
                        for(int i=0;i<jsonArray.length();i++) {
                            JSONObject no = jsonArray.getJSONObject(i);
                            spinnerRowArrayList.add(new SpinnerRow(no.getString("id"),no.getString("gender")));
                        }
                        runOnUiThread(() -> {
                            SpinnerRowAdapter spinnerRowAdapter=new SpinnerRowAdapter(RegistrationActivity.this,spinnerRowArrayList);
                            spinGender.setAdapter(spinnerRowAdapter);
                            spinnerRowAdapter.notifyDataSetChanged();

                        });

                    } catch (JSONException e) {
                        e.printStackTrace();
                        System.out.print(e.toString());
                    }
                    if(response.isSuccessful()) {
                        runOnUiThread(() -> {

                        });
                    }
                }
            });
        }
    }
```
