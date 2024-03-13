import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.os.Bundle;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(new SquareView(this));
    }

    private static class SquareView extends View {
        private Paint paint;

        public SquareView(Context context) {
            super(context);
            paint = new Paint();
            paint.setColor(Color.BLACK);
            paint.setStyle(Paint.Style.STROKE);
            paint.setStrokeWidth(5);
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);
            int sideLength = 200; // Długość boku kwadratu
            int centerX = getWidth() / 2; // Środek widoku w poziomie
            int centerY = getHeight() / 2; // Środek widoku w pionie

            // Rysowanie kwadratu
            int halfSide = sideLength / 2;
            int left = centerX - halfSide;
            int top = centerY - halfSide;
            int right = centerX + halfSide;
            int bottom = centerY + halfSide;
            canvas.drawRect(left, top, right, bottom, paint);
        }
    }
}
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <com.example.yourpackage.SquareView
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</FrameLayout>
