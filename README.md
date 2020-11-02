# Test-ABC
testKiemTra
#View 1

public class MainActivity extends AppCompatActivity {

    EditText HoTen;
    EditText NgaySinh;
    Button btSubmit;
    Button btNhap;
    TextView tvKq1;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        HoTen=(EditText)findViewById(R.id.edHoTen);
        NgaySinh=(EditText)findViewById(R.id.edNgaySinh);
        btSubmit=(Button) findViewById(R.id.btSubmit);
        btNhap=(Button) findViewById(R.id.btNhap);
        tvKq1=(TextView) findViewById(R.id.tvkkk);

        btSubmit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String hotenx=HoTen.getText().toString();
                String namsinhx=NgaySinh.getText().toString();
                Intent intent=new Intent(MainActivity.this,Main2Activity.class);
                intent.putExtra("ht",hotenx);
                intent.putExtra("ns",namsinhx);
                startActivity(intent);
            }
        });

        btNhap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent=new Intent(MainActivity.this,Main2Activity.class);
                startActivityForResult(intent,9999);

            }
        });
    }
    @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(requestCode == 9999 )
        {
            if(resultCode == RESULT_OK) {
                String hoten = data.getStringExtra("hten");
                int namsinh = Integer.parseInt(data.getStringExtra("nsinh"));
                String kq = "Họ và tên" + hoten;
                kq += "\n Nam sinh" + namsinh;
                tvKq1.setText(kq);
            }
            else
            {
                tvKq1.setText("No");

            }
        }


    }
}

#View 2

public class Main2Activity extends AppCompatActivity {

    TextView tvKQ;
    Button Exit;
    EditText edTen;
    EditText edNS;
    Button btnSubmit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        tvKQ=(TextView) findViewById(R.id.tvKQ);
        Exit=(Button) findViewById(R.id.btExit);
        edNS=(EditText) findViewById(R.id.edDate);
        edTen=(EditText) findViewById(R.id.edName);
        btnSubmit=(Button) findViewById(R.id.btnFinish);
        /*
        String horten= getIntent().getStringExtra("ht");
        int naming=Integer.parseInt( getIntent().getStringExtra("ns"));
        String kq="Họ và tên" +horten;
        kq+="\n Nam sinh"+ naming;
        tvKQ.setText(kq);
         */
        Exit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                finish();
            }
        });
        btnSubmit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent=new Intent();
                intent.putExtra("hten",edTen.getText().toString());
                intent.putExtra("nsinh",edNS.getText().toString());
                setResult(RESULT_OK,intent);
                finish();
            }
        });
    }

    public  void  onBackPressed(){
        setResult(Activity.RESULT_CANCELED);
        super.onBackPressed();
    }
}
# GiuaKy
#Xử lý ghi dữ liệu vào bộ nhớ trong
----------------------------------------------------------------------
OutputStream os = openFileOutput("FileName", MODE_APPEND/MODE_PRIVATE);
String str = "Dữ liệu cần ghi";
os.write(str.getBytes());
os.close();
#Xử lý đọc dữ liệu từ bộ nhớ trong 
-----------------------------------------------------------------------
FileInputStream fis = openFileInput("fileName");
BufferedReader br = new BufferedReader(new InputStreamReader(fis));
StringBuffer data = new StringBuffer();
String line = "";
while ((line = br.readLine()) != null) {
 data. append(line).append("\n");
}
#Xử lý ghi dữ liệu vào bộ nhớ ngoài
-----------------------------------------------------------------------
File sdcard = Environment.getExternalStorageDirectory();
File file = new File(sdcard,"FileName");
OutputStream os = new FileOutputStream(file);
String str = "Dữ liệu muốn ghi";
os.write(str.getBytes());
os.close();
#Xử lý đọc dữ liệu từ bộ nhớ ngoài
-----------------------------------------------------------------------
File sdcard = Environment.getExternalStorageDirectory();
File file = new File(sdcard,"FileName");
BufferedReader br = new BufferedReader(new FileReader(file));
String line;
//Đọc dữ liệu từ file, nội dung sau khi đọc sẽ chứa trong biến content
StringBuilder content = new StringBuilder();
while ((line = br.readLine()) != null) {
 content.append(line);
 content.append('\n');
}
br.close();
#Shared Preferences
-------------------------------------------------------------------
SharedPreferences sp = getSharedPreferences("FileName", Mode);
1	MODE_APPEND Nối preferences mới với preferences đã tồn tại
2	MODE_PRIVATE Chỉ được truy cập cục bộ
3	MODE_WORLD_READABLE Chế độ này cho phép ứng dụng khác đọc preferences
4	MODE_WORLD_WRITEABLE Chế độ này cho phép ứng dụng khác ghi preferences
//Tạo đối tượng SharedPreferences
SharedPreferences sp = getSharedPreferences("FileName", Mode);
SharedPreferences.Editor editor = sp.edit();
//Lưu dữ liệu
editor.putX(key, value); //X là kiểu dữ liệu
//Hoàn thành
editor.commit();
//Đọc dữ liệu
sp.getX(key, default); //X là kiểu dữ liệu
