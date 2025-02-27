import java.util.*;

class SocialMediaMonetization {
    static User[] users = new User[10];
    static Post[] posts = new Post[20];
    static int userCount = 0;
    static int postCount = 0;
    static Scanner scanner = new Scanner(System.in);
    static Random random = new Random();

    public static void main(String[] args) 
	{
        while (true) {
            System.out.println("\n--- Social Media Monetization Platform ---\n");
            System.out.println("1. Register");
            System.out.println("2. Login");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    registerUser();
                    break;
                case 2:
                    loginUser();
                    break;
                case 3:
                    System.out.println("Exiting application...");
                    System.exit(0);
                default:
                    System.out.println("Invalid option. Try again.");
            }
        }
    }

    static void registerUser()
	{
        if (userCount >= users.length) {
            System.out.println("User limit reached. Cannot register more users.");
            return;
        }
        System.out.print("Enter username: ");
        String username = scanner.next();

        System.out.print("Enter password: ");
        String password = scanner.next();

        users[userCount++] = new User(username, password, "Creator");
        System.out.println(" Account created successfully!");
    }

    static void loginUser() 
	{
        System.out.print("Enter username: ");
        String username = scanner.next();
        System.out.print("Enter password: ");
        String password = scanner.next();

        for (int i = 0; i < userCount; i++)
			{
              if (users[i].getUsername().equals(username) && users[i].checkPassword(password)) {
                int otp = generateOTP();
				System.out.println("  ");
                System.out.println("Your OTP is: "+otp+" " );
				System.out.println("   ");
				
                System.out.print("Enter OTP below: ");
                int enteredOTP = scanner.nextInt();

                if (enteredOTP == otp)
					{
                    System.out.println(" Login successful!");
                    mainMenu(users[i]);
                     } 
				else 
				{
                    System.out.println(" Invalid OTP !  . Login failed.");
                }
                return;
            }
        }
        System.out.println("Invalid username or password.");
    }

    static int generateOTP()
	{
        return 1000 + random.nextInt(9000);
    }

    static void mainMenu(User user)
	{
        while (true) {
            System.out.println("\n--- Main Menu ---");
            System.out.println("1. Create Post");
            System.out.println("2. View Posts");
            System.out.println("3. View Analytics");
            System.out.println("4. Manage Monetization");
            System.out.println("5. Process Payments");
            System.out.println("6. Logout");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    createPost();
                    break;
                case 2:
                    viewPosts();
                    break;
                case 3:
                    viewAnalytics();
                    break;
                case 4:
                    manageMonetization();
                    break;
                case 5:
                    processPayments(user);
                    break;
                case 6:
                    System.out.println("Logging out...");
                    return;
                default:
                    System.out.println("Invalid option. Try again.");
            }
        }
    }

    static void createPost()
	{
        if (postCount >= posts.length) 
		{
            System.out.println("Post limit reached. Cannot create more posts.");
            return;
        }

        System.out.println("Enter post title: ");
        scanner.nextLine();
        String title = scanner.nextLine();
        System.out.println("Enter post content type(ex.Educational/information/review): ");
        String content = scanner.nextLine();

        posts[postCount++] = new Post(title, content);
        System.out.println("Post created successfully!");
    }

    static void viewPosts()
	{
        System.out.println("--- All Posts ---");
        for (int i = 0; i < postCount; i++)
			{
            System.out.println("Title: " + posts[i].getTitle());
            System.out.println("Content type: " + posts[i].getContent());
            System.out.println();
        }
    }

    static void viewAnalytics() 
	{
    System.out.println("\n--- Analytics ---");
    System.out.println("Total Users: " + userCount);
    System.out.println("Total Posts: " + postCount);

    if (postCount == 0) {
        System.out.println("No posts available for analysis.");
        return;
    }

    int totalViews = 0;
    double maxEarnings = 0, minEarnings = Double.MAX_VALUE, totalEarnings = 0;
    int maxViews = 0, minViews = Integer.MAX_VALUE;
    String topPost = "", leastViewedPost = "";

    for (int i = 0; i < postCount; i++)
		{
        int views = (int) (Math.random() * (1000000 - 1000 + 1)) + 1000;
        double earnings = (views / 1000) * 5;
        totalViews += views;
        totalEarnings += earnings;

        if (views > maxViews) 
		{
            maxViews = views;
            topPost = posts[i].getTitle();
        }
        if (views < minViews) 
		{
            minViews = views;
            leastViewedPost = posts[i].getTitle();
        }

        if (earnings > maxEarnings)
			{
            maxEarnings = earnings;
        }
        if (earnings < minEarnings)
			{
            minEarnings = earnings;
        }
    }

    System.out.println("Total Views: " + totalViews);
    System.out.println("Average Views per Post: " + (totalViews / postCount));
    System.out.println("Most Viewed Post: " + topPost + " (" + maxViews + " views)");
    System.out.println("Least Viewed Post: " + leastViewedPost + " (" + minViews + " views)");
    System.out.println("Total Earnings: $" + totalEarnings);
    System.out.println("Highest Earning Post: $" + maxEarnings);
    System.out.println("Lowest Earning Post: $" + minEarnings);
}

    static double totalEarnings = 0;
    static void manageMonetization() 
	{
        System.out.println("--- Manage Monetization ---");
        totalEarnings = 0;
        for (int i = 0; i < postCount; i++)
			{
            int views = (int) (Math.random() * (1000000 - 1000 + 1)) + 1000;
            double earnings = (views / 1000) * 5;
            totalEarnings += earnings;
            System.out.println("Post: " + posts[i].getTitle());
            System.out.println("Views Counted: " + views);
            System.out.println("Earnings: " + earnings + "$\n");
        }
		
        System.out.println("Total Earnings Across All Posts: $" + totalEarnings);
    }

    static void processPayments(User user)
	{
    System.out.println("--- Process Payments ---");
    System.out.println("Processing payment for: " + user.getUsername());
    System.out.println("Total Earnings to be Paid: $" + totalEarnings);

    if (totalEarnings <= 0) 
	{
        System.out.println("No earnings available for payment.");
        return;
    }

    System.out.println("Select Payment Method:");
    System.out.println("1. Bank Transfer");
    System.out.println("2. PayPal");
    System.out.println("3. UPI");
    System.out.print("Enter your choice: ");
    int paymentChoice = scanner.nextInt();
String paymentMethod = null;  // Initialize the variable before the switch

switch (paymentChoice) 
{
    case 1:
        paymentMethod = "Bank Transfer";
        break;
    case 2:
        paymentMethod = "PayPal";
        break;
    case 3:
        paymentMethod = "UPI";
        break;
    default:
        System.out.println("Invalid choice. Payment canceled.");
        return;  // Exit the method if an invalid choice is made
}

if (paymentMethod == null) return;  // Extra safety check

System.out.print("Confirm Payment? (yes/no): ");
String confirmation = scanner.next();
if (!confirmation.equalsIgnoreCase("yes"))
	{
    System.out.println("Payment canceled.");
    return;
}

System.out.println("Payment of $" + totalEarnings + " processed successfully via " + paymentMethod + "!");
totalEarnings = 0;  // Reset earnings after payment

   

}
}
class User 
{
    String username;
    String password;
    String role;

    public User(String username, String password, String role) 
	{
        this.username = username;
        this.password = password;
        this.role = role;
    }

    public String getUsername() {
        return username;
    }

    public boolean checkPassword(String password) {
        return this.password.equals(password);
    }
}

class Post {
    String title;
    String content;

    public Post(String title, String content) {
        this.title = title;
        this.content = content;
    }

    public String getTitle() {
        return title;
    }

    public String getContent() {
        return content;
    }
}
