# Unit-3-linked-list
To implement a music playlist using a circular linked list
#include <iostream>
#include <string>
using namespace std;

struct Song {
    string name;
    Song* next;
};

class MusicPlaylist {
    Song* head;

public:
    MusicPlaylist() {
        head = NULL;
    }

    void addSong(string songName) {
        Song* newSong = new Song;
        newSong->name = songName;

        if (head == NULL) {
            head = newSong;
            newSong->next = head;
        } else {
            Song* temp = head;

            while (temp->next != head) {
                temp = temp->next;
            }

            temp->next = newSong;
            newSong->next = head;
        }

        cout << "Song added successfully!\n";
    }

    void displayPlaylist() {
        if (head == NULL) {
            cout << "Playlist is empty!\n";
            return;
        }

        Song* temp = head;

        cout << "\nMusic Playlist:\n";

        do {
            cout << temp->name << endl;
            temp = temp->next;
        } while (temp != head);
    }

    void playSongs() {
        if (head == NULL) {
            cout << "No songs to play!\n";
            return;
        }

        Song* temp = head;
        char choice;

        do {
            cout << "\nNow Playing: " << temp->name << endl;
            cout << "Next song? (y/n): ";
            cin >> choice;

            if (choice == 'y' || choice == 'Y') {
                temp = temp->next;
            } else {
                break;
            }
        } while (true);
    }
};

int main() {
    MusicPlaylist playlist;
    int choice;
    string songName;

    do {
        cout << "\n--- MUSIC PLAYLIST ---\n";
        cout << "1. Add Song\n";
        cout << "2. Display Playlist\n";
        cout << "3. Play Songs\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter song name: ";
                getline(cin >> ws, songName);
                playlist.addSong(songName);
                break;

            case 2:
                playlist.displayPlaylist();
                break;

            case 3:
                playlist.playSongs();
                break;

            case 4:
                cout << "Exiting Music Playlist...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }
    } while (choice != 4);

    return 0;
}
