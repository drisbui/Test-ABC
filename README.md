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
