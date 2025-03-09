# Social-media-notifications-and-alerts
class Notification:
    def _init_(self, message):
        self.message = message
        self.next = None

class NotificationQueue:
    def _init_(self):
        self.queue = []

    def add_notification(self, notification):
        self.queue.append(notification)

    def view_notifications(self):
        return [notification.message for notification in self.queue]

    def remove_notification(self):
        if self.queue:
            return self.queue.pop(0)
        return None

class MessagingSystem:
    def _init_(self):
        self.conversations = {}

    def send_message(self, sender, receiver, content):
        conversation_key = tuple(sorted([sender, receiver]))
        if conversation_key not in self.conversations:
            self.conversations[conversation_key] = []
        message = f"{sender}: {content}"
        self.conversations[conversation_key].append(message)

    def view_messages(self, user1, user2):
        conversation_key = tuple(sorted([user1, user2]))
        return self.conversations.get(conversation_key, ["No messages available."])

def main():
    queue = NotificationQueue()
    messaging = MessagingSystem()

    while True:
        print("\nChat and Notification System")
        print("1. Add Notification")
        print("2. View Notifications")
        print("3. Remove Notification")
        print("4. Send Message")
        print("5. View Conversation")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            message = input("Enter notification message: ")
            queue.add_notification(Notification(message))

        elif choice == '2':
            print("Queue Notifications:", queue.view_notifications())

        elif choice == '3':
            removed = queue.remove_notification()
            print("Removed from Queue:", removed.message if removed else "No notifications to remove.")

        elif choice == '4':
            sender = input("Enter sender name: ")
            receiver = input("Enter receiver name: ")
            content = input("Enter message: ")
            messaging.send_message(sender, receiver, content)

        elif choice == '5':
            user1 = input("Enter first user name: ")
            user2 = input("Enter second user name: ")
            print("Conversation:", messaging.view_messages(user1, user2))

        elif choice == '6':
            print("Exiting...")
            break

        else:
            print("Invalid choice. Please try again.")

if _name_ == "_main_":
    main()
