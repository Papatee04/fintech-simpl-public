Simpl – Fintech Mobile App
Simpl is a mobile payment application developed using Flutter for the frontend and Django for the backend, with integration of Visa Direct APIs for secure, real-time payment processing. The app is designed for an intuitive user experience and enables users to make payments quickly and securely.

Key Features
Real-time Payments: Visa Direct integration allows users to initiate and process payments securely.
User Authentication: Secure login and registration, with backend support via Django.
Transaction History: Users can view their transaction history, including details such as sender, receiver, amount, and status.
Intuitive UI: Built with Flutter, the app offers a seamless and easy-to-navigate user experience.
Technology Stack
Frontend: Flutter
Backend: Django, Django REST Framework
Payment Integration: Visa Direct APIs
Database: PostgreSQL (or specify the database you're using)
Hosting: Azure
API Endpoints
Here is an example of the API for viewing a user's transaction history:

python
Copy code
@login_required
def view_transaction_history(request):
    user = request.user

    # Fetch transactions for the logged-in user
    transactions = Transaction.objects.filter(sender=user) | Transaction.objects.filter(
        receiver=user).select_related('sender', 'receiver', 'card', 'wallet')

    transaction_history = {
        'transactions': [
            {
                'type': transaction.transaction_type,
                'sender': transaction.sender.username,
                'receiver': transaction.receiver.username,
                'amount': str(transaction.amount),
                'timestamp': transaction.timestamp.strftime('%Y-%m-%d %H:%M:%S'),
                'status': transaction.status,
                'additional_info': transaction.get_additional_info(),
            }
            for transaction in transactions
        ],
    }

    return JsonResponse({'status': 'success', 'transaction_history': transaction_history})
The app includes additional admin operations for managing transactions, such as adding, editing, categorizing, and deleting transactions. These operations can be managed via the Django admin dashboard for ease of use.

Screenshots
You can view the app's UI through the screenshots below:

Home Screen

Transaction History

Payment Flow

Installation & Setup
Clone the repository:

bash
Copy code
git clone https://github.com/your-username/simpl-fintech-app.git
cd simpl-fintech-app
Install the required dependencies:

For Flutter:
bash
Copy code
flutter pub get
For Django:
bash
Copy code
pip install -r requirements.txt
Run the backend server:

bash
Copy code
python manage.py runserver
Run the Flutter app:

bash
Copy code
flutter run
License
This project is licensed under the MIT License. See the LICENSE file for details.

