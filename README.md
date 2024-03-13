import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.LinearLayout;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        LinearLayout layout = findViewById(R.id.layout);

        // Dodanie widoku sześcianu do layoutu
        CubeView cubeView = new CubeView(this);
        LinearLayout.LayoutParams layoutParams = new LinearLayout.LayoutParams(
                ViewGroup.LayoutParams.MATCH_PARENT,
                ViewGroup.LayoutParams.MATCH_PARENT
        );
        layout.addView(cubeView, layoutParams);
    }
}
aaaaaa cube
import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.view.View;

public class CubeView extends View {

    private Paint paint;
    private Path path;

    public CubeView(Context context) {
        super(context);
        paint = new Paint();
        paint.setColor(Color.RED);
        paint.setStyle(Paint.Style.FILL);
        path = new Path();
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);

        int centerX = getWidth() / 2;
        int centerY = getHeight() / 2;

        int size = 200; // Rozmiar sześcianu

        // Rysowanie sześcianu
        path.reset();
        // Górna ściana
        path.moveTo(centerX - size / 2, centerY - size / 2);
        path.lineTo(centerX + size / 2, centerY - size / 2);
        path.lineTo(centerX + size / 4, centerY - size);
        path.lineTo(centerX - size / 4, centerY - size);
        path.close();
        // Boczna ściana
        path.moveTo(centerX + size / 2, centerY - size / 2);
        path.lineTo(centerX + size / 4, centerY - size);
        path.lineTo(centerX + size / 4, centerY + size / 2);
        path.lineTo(centerX + size / 2, centerY + size / 4);
        path.close();
        // Inne ściany analogicznie

        canvas.drawPath(path, paint);
    }
}
xml 
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/container"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.example.myapplication.CubeView
        android:id="@+id/cube_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</RelativeLayout>
