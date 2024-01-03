# AMID
Projekty z lekcji
import android.os.Bundle;
import android.os.Handler;
import android.widget.TextView;

import androidx.appcompat.app.AppCompatActivity;

import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.Locale;

public class CountdownActivity extends AppCompatActivity {

    private TextView countdownTextView;
    private TextView currentDateTimeTextView;
    private Handler handler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_countdown);

        countdownTextView = findViewById(R.id.countdownTextView);
        currentDateTimeTextView = findViewById(R.id.currentDateTimeTextView);
        handler = new Handler();

        // Uruchom odliczanie co sekundę
        handler.postDelayed(updateTimeRunnable, 1000);
    }

    private Runnable updateTimeRunnable = new Runnable() {
        @Override
        public void run() {
            updateDateTime();
            updateCountdown();
            handler.postDelayed(this, 1000); // Uruchom ponownie co sekundę
        }
    };

    private void updateDateTime() {
        SimpleDateFormat dateTimeFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.getDefault());
        String currentDateTime = dateTimeFormat.format(new Date());
        currentDateTimeTextView.setText("Aktualna data i czas: " + currentDateTime);
    }

    private void updateCountdown() {
        // Ustal datę końca roku
        Calendar calendar = Calendar.getInstance();
        calendar.set(Calendar.YEAR, calendar.get(Calendar.YEAR) + 1); // Przejście na kolejny rok
        calendar.set(Calendar.MONTH, Calendar.JANUARY);
        calendar.set(Calendar.DAY_OF_MONTH, 1);
        calendar.set(Calendar.HOUR_OF_DAY, 0);
        calendar.set(Calendar.MINUTE, 0);
        calendar.set(Calendar.SECOND, 0);
        calendar.set(Calendar.MILLISECOND, 0);

        Date endDate = calendar.getTime();

        // Oblicz czas do końca roku
        long currentTime = System.currentTimeMillis();
        long endTime = endDate.getTime();
        long timeDifference = endTime - currentTime;

        // Wyświetl czas do końca roku
        SimpleDateFormat countdownFormat = new SimpleDateFormat("dd:HH:mm:ss", Locale.getDefault());
        String formattedTime = countdownFormat.format(new Date(timeDifference));
        countdownTextView.setText("Czas do końca roku: " + formattedTime);
    }
}
