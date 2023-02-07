# code
import java.util.Date;
import java.util.Scanner;

class Clock {
    int hours;
    int minutes;
    int seconds;
    int days;

    Clock() {
        hours = 12;
        minutes = 0;
        seconds = 0;
    }

    Clock(int hours, int minutes, int seconds) {
        this.hours = hours;
        this.minutes = minutes;
        this.seconds = seconds;
    }

    Clock(int seconds) {
        int Sec = seconds;
        int Hou = Sec / 60;
        int Min = Hou % 60;
        Hou = Hou / 60;
        // this.hours = Hou;
        // this.minutes = Min;
        // this.seconds = Sec / 3600; 
    }

    public void setClock(int seconds) {
        int Sec = seconds;
        int Hou = Sec / 60;
        int Min = Hou % 60;
        Hou = Hou / 60;
        this.hours = Hou;
        this.minutes = Min;
        this.seconds = Sec/3600; 
    }

    public int getHours() {
        return this.hours;
    }

    public int getMinutes() {
        return this.minutes;
    }

    public int getSeconds() {
        return this.seconds;
    }

    public void setHours(int hours) {
        this.hours = hours;
    }

    public void setMinutes(int minutes) {
        this.minutes = minutes;
    }

    public void setSeconds(int seconds) {
        this.seconds = seconds;
    }

    public void tick() {
        if(this.hours > 24){
            this.days += 1;
            this.hours = 0;
        }
        if(this.minutes > 59){
            this.hours += 1;
            this.minutes = 0;
        }
        if (this.seconds > 59) {
            this.minutes += 1;
            this.seconds = 0;
        } else {
            this.seconds++;
        }
       
    }

    void addClock(Clock c1)
    {
       
        this.seconds=this.seconds+c1.seconds;
        if(this.seconds>59)
        {
            this.seconds=this.seconds%60;
            this.minutes+=1;
        }
        
        this.minutes=this.minutes+c1.minutes;
        if(this.minutes>59)
        {
            this.minutes=this.minutes%60;
            this.hours+=1;
        }
        this.hours=this.hours+c1.hours;
        if(this.hours>23)
        {
            this.hours=this.hours%24;
            this.days+=1;;
        }

    }

    public String toStringg() {
        return "Day::"+ this.days + ": " + this.hours + ":" + this.minutes + ":" + this.seconds;
    }

    public void tickDown() {
        if(this.hours <= 0){
            this.days += -1;
            this.hours = 60;
        }
        if(this.minutes <= 0){
            this.hours += -1;
            this.minutes = 60;
        }
        if (this.seconds <= 0) {
            this.minutes += -1;
            this.seconds = 60;
        } else {
            this.seconds--;
        }
    }

    public Clock subtractClock(Clock obj) {
        int hou = this.hours - obj.hours;
        int min = this.minutes - obj.minutes;
        int sec = this.seconds - obj.seconds;
        return new Clock(hou, min, sec);
    }
}


public class ClockDemo {
    public static void main(String[] args) {
        int sec;
        Scanner in = new Scanner(System.in);

        System.out.println("Enter no. of seconds: ");
        sec = in.nextInt();
        Clock firstClock = new Clock(sec);

        System.out.println("Time: -> " + firstClock.toStringg());

        for (int i = 0; i < 10; i++) {
            firstClock.tick();
            System.out.print(" Tick" + (i + 1) + ": " + firstClock.toStringg() + '\t');
        }
        System.out.println();
        System.out.println();

        int hour;
        System.out.println("Enter hour(0-23): ");
        hour = in.nextInt();
        if(hour > 24){
            throw new Error("Hour can't more than 24");
        }
       
        int minute;
        System.out.println("Enter minute(0-59): ");
        minute = in.nextInt();
        if(minute > 24){
            throw new Error("minute can't more than 60");
        }

        int second;
        System.out.println("Enter second(0-59): ");
        second = in.nextInt();
        if(second > 24){
            throw new Error("seconds can't more than 60");
        }

        Clock secondClock = new Clock(hour, minute, second);
        System.out.println("Time: ->" + secondClock.toStringg());

        for (int i = 0; i < 10; i++) {
            secondClock.tickDown();
            System.out.print(" Tickdown" + (i + 1) + ": " + secondClock.toStringg() + '\t');
        }
        System.out.println();
        System.out.println();

        firstClock.addClock(secondClock);
        System.out.println("firstClock: " + firstClock.toStringg());
        System.out.println("secondClock: " + secondClock.toStringg());

        Clock thirdClock = firstClock.subtractClock(secondClock);
        System.out.println(thirdClock.toStringg());

    }
}
