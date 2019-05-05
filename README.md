 # GitTools
Just another repository 
package com.mctcollege.assignment;

import android.content.Intent;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.security.PublicKey;

public class FirstActivity extends AppCompatActivity {
    EditText editText;
    Button STbutton, SPDEbutton, StTbutton, StPDFbutton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_first);


        editText = (EditText) findViewById(R.id.editText);
        STbutton = (Button) findViewById(R.id.STbutton);
        SPDEbutton = (Button) findViewById(R.id.SPDEbutton);
        StTbutton = (Button) findViewById(R.id.StTbutton);
        StPDFbutton = (Button) findViewById(R.id.StPDFbutton);

        STbutton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {


                String massage = editText.getText().toString();
                try {
                    OutputStreamWriter out = new OutputStreamWriter(openFileOutput("text.txt", 0));
                    out.write(editText.getText().toString());
                    out.close();
                    Toast.makeText(FirstActivity.this, "Text  saved as Text ", Toast.LENGTH_LONG)
                            .show();
                } catch (Throwable t) {
                    Toast.makeText(FirstActivity.this, "Exception: " + t.toString(), Toast.LENGTH_LONG).show();
                }
            }
        });
        SPDEbutton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String massage = editText.getText().toString();
                try {
                    OutputStreamWriter out = new OutputStreamWriter(openFileOutput("text.pdf", 0));
                    out.write(editText.getText().toString());
                    out.close();
                    Toast.makeText(FirstActivity.this, "Text saved as PDF ", Toast.LENGTH_LONG)
                            .show();
                } catch (Throwable t) {
                    Toast.makeText(FirstActivity.this, "Exception: " + t.toString(), Toast.LENGTH_LONG).show();

                }
            }
        });

        StTbutton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String a = editText.getText().toString();
                if (a != null) {
                    showtext();
                } else {
                    Toast.makeText(FirstActivity.this, "Please Enter your text ", Toast.LENGTH_LONG).show();
                }
            }
        });
        StPDFbutton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (editText != null)
                    showpdf();

                else {
                    Toast.makeText(FirstActivity.this, "Please Enter your text ", Toast.LENGTH_LONG).show();
                }
            }
        });
    }

    public void showtext() {
        try {

            InputStream in = openFileInput("text.txt");
            if (in != null) {
                InputStreamReader tmp = new InputStreamReader(in);
                BufferedReader reader = new BufferedReader(tmp);
                String str;
                StringBuilder buf = new StringBuilder();
                while ((str = reader.readLine()) != null) {
                    buf.append(str + "n");
                }
                in.close();

                Intent intent = new Intent(FirstActivity.this, SecondActivity.class);
                intent.putExtra("message", editText.getText().toString());
                startActivityForResult(intent, 11);
                editText.setText("");
            }
        } catch (Exception a) {
            a.printStackTrace();
        }
    }

    public void showpdf() {
        try {
            InputStream in = openFileInput("text.pdf");
            if (in != null) {
                InputStreamReader tmp = new InputStreamReader(in);
                BufferedReader reader = new BufferedReader(tmp);
                String str;
                StringBuilder buf = new StringBuilder();
                while ((str = reader.readLine()) != null) {
                    buf.append(str + "n");
                }
                in.close();

                Intent intent = new Intent(FirstActivity.this, ThirdActivity.class);
                intent.putExtra("message", editText.getText().toString());
                startActivityForResult(intent, 11);
                editText.setText("");
            }
        } catch (Exception a) {
            a.printStackTrace();
            Toast.makeText(FirstActivity.this, "Please Enter your text ", Toast.LENGTH_LONG).show();
        }
    }
}




