# GetImageFromGallery

### Priview
![getimage](https://user-images.githubusercontent.com/43386555/58547040-d5e35f80-8230-11e9-8e4d-476b31b60f0b.gif)

### 1. mainactivity.xml
     <ImageView
        android:id="@+id/image_profile"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:layout_marginTop="132dp"
        android:src="@drawable/image_profile"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
        
### 2. MainActivity.java
      public class MainActivity extends AppCompatActivity {

          ImageView image_profile; //global variable
          private static final int PICK_IMAGE = 1;
          Uri imageUri;

          @Override
          protected void onCreate(Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.activity_main);

              image_profile = (ImageView) findViewById(R.id.image_profile);

              image_profile.setOnClickListener(new View.OnClickListener() {
                  @Override
                  public void onClick(View v) {

                      Intent gallery = new Intent();
                      gallery.setType("image/*");
                      gallery.setAction(Intent.ACTION_GET_CONTENT);

                      startActivityForResult(Intent.createChooser(gallery, "Sellect picture"), PICK_IMAGE);
                  }
              });
          }

          //option + enter onActivityResult
          @Override
          protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
              super.onActivityResult(requestCode, resultCode, data);

              if (requestCode == PICK_IMAGE && resultCode == RESULT_OK)
              {
                  imageUri = data.getData();
                  try
                  {
                      Bitmap bitmap = MediaStore.Images.Media.getBitmap(getContentResolver(), imageUri);
                      image_profile.setImageBitmap(bitmap);
                  }
                  catch (IOException e)
                  {
                      e.printStackTrace();
                  }
              }
          }
      }
