# Cambios de pantalla

### Activity code
```bach
 public void cambiar(View view){
        //intent
        Intent sig = new Intent(this,secondView.class);
        startActivity(sig);
    }
```


# Manejo de variables

### Activity code 

```bach 
public class MainActivity extends AppCompatActivity {

    private EditText v1;
    TextView showText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        v1 = (EditText) findViewById(R.id.inputText);
        showText = findViewById(R.id.textView2);
    }

}

```


# Envio de datos entre activity

### Activity 1 design

![image](https://user-images.githubusercontent.com/74383095/192413381-60201d66-49ba-4223-b220-428bfbf5e665.png)


### ACtivity 1 code

```bach
public class MainActivity extends AppCompatActivity {

    private EditText v1;
    private EditText v2;
    private RadioButton suma;
    private RadioButton resta;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        v1 = findViewById(R.id.num1);
        v2 = findViewById(R.id.num2);

        suma = findViewById(R.id.sum);
        resta = findViewById(R.id.rest);
    }

    public void cambiar(View view){
        Intent sig = new Intent(this, MainActivity2.class);

        String value1 = v1.getText().toString();
        String value2 = v2.getText().toString();

        int val1 = Integer.parseInt(value1);
        int val2 = Integer.parseInt(value2);

        if (suma.isChecked() == true){
            int sum = val1 + val2;
            String res = String.valueOf(sum);
            sig.putExtra("dato", res);
            startActivity(sig);
        }else{
            int rest = val1 - val2;
            String res = String.valueOf(rest);
            sig.putExtra("dato", res);
            startActivity(sig);
        }

    }
}

```


### Activity 2 design

![image](https://user-images.githubusercontent.com/74383095/192413678-9337a3c1-7547-4fa4-b213-2c5e4fbec22a.png)

### Activity 2 code 

```bach 
public class MainActivity2 extends AppCompatActivity {

    private TextView r;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        r = findViewById(R.id.txt1);

        String value = getIntent().getStringExtra("dato");
        r.setText(value);
    }
}

```




# Almacenamiento de datos con sharedpreferences

### Activity design

![image](https://user-images.githubusercontent.com/74383095/192411747-9d793289-5dbc-4d5f-a29e-0a20efd50a98.png)

### Activity code
```bach
package com.example.almacenamientodatos;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private EditText txt1;
    private EditText txt2;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        txt1 = (EditText) findViewById(R.id.txt1);
        txt2 = (EditText) findViewById(R.id.txt2);
    }

    public void save (View view){
        String name = txt1.getText().toString();
        String info = txt2.getText().toString();

        SharedPreferences preferences = getSharedPreferences("contactList", Context.MODE_PRIVATE);
        SharedPreferences.Editor obj_editor = preferences.edit();
        obj_editor.putString(name, info);
        obj_editor.commit();

        Toast.makeText(this, "Contact saved", Toast.LENGTH_SHORT).show();
    }


    public void search (View view){
        String name = txt1.getText().toString();

        SharedPreferences preferences = getSharedPreferences("contactList", Context.MODE_PRIVATE);
        String data = preferences.getString(name, "");

        if(data.length() == 0){
            Toast.makeText(this, "Contact not found", Toast.LENGTH_SHORT).show();
        }else{
            txt2.setText(data);
        }
    }
}

```

# Mensajes emergentes (Toast)

```bach
Toast.makeText(this, "Contact saved", Toast.LENGTH_SHORT).show();

```


# Artchivos string

```bach
<resources>
    <string name="app_name">My Application</string>
    <string name="txt1">Number 1</string>
    <string name="txt2">Number 2</string>
    <string name="txt3">Sumar</string>
    <string name="txt4">Restar</string>
    <string name="txt5">Calculate</string>
</resources>

```


