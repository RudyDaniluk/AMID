import android.animation.ObjectAnimator;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private ImageView squareImage;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        squareImage = findViewById(R.id.square_image);

        Button startButton = findViewById(R.id.start_button);
        startButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startAnimation();
            }
        });
    }

    private void startAnimation() {
        ObjectAnimator animator = ObjectAnimator.ofFloat(squareImage, "rotation", 0f, 360f);
        animator.setDuration(2000); // Ustaw czas trwania animacji w milisekundach
        animator.setRepeatCount(ObjectAnimator.INFINITE); // Ustaw powtórzenia na nieskończoność
        animator.start();
    }
}
