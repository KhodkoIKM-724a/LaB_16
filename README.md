#include <iostream>
#include <string>
#include <vector>
#include <locale>
#include <windows.h>

class Magazine {
private:
    std::wstring title;
    std::wstring publisher;
    int year;
    int pages;

public:
    Magazine(std::wstring t, std::wstring p, int y, int pg)
        : title(t), publisher(p), year(y), pages(pg) {
    }

    int getYear() const { return year; }
    std::wstring getPublisher() const { return publisher; }

    void print() const {
        std::wcout << L"Назва: " << title << std::endl;
        std::wcout << L"Видавництво: " << publisher << std::endl;
        std::wcout << L"Рік: " << year << std::endl;
        std::wcout << L"Сторінки: " << pages << std::endl;
        std::wcout << L"----------------------\n";
    }
};

void printByPublisher(const std::vector<Magazine>& magazines, const std::wstring& targetPublisher) {
    std::wcout << L"\nЖурнали видавництва \"" << targetPublisher << L"\":\n";
    for (const auto& mag : magazines) {
        if (mag.getPublisher() == targetPublisher) {
            mag.print();
        }
    }
}

void printAfterYear(const std::vector<Magazine>& magazines, int yearThreshold) {
    std::wcout << L"\nЖурнали, випущені після " << yearThreshold << L" року:\n";
    for (const auto& mag : magazines) {
        if (mag.getYear() > yearThreshold) {
            mag.print();
        }
    }
}

int main() {
    system("chcp 65001 > nul");
    setlocale(LC_ALL, "");

    std::vector<Magazine> magazines = {
        Magazine(L"Наука і життя", L"Наукове", 2020, 120),
        Magazine(L"Техніка молоді", L"ТехПрес", 2018, 90),
        Magazine(L"Дослідник", L"Наукове", 2022, 100),
        Magazine(L"Світ знань", L"Освіта", 2021, 80)
    };

    std::wstring searchPublisher;
    int searchYear;

    std::wcout << L"Введіть назву видавництва для пошуку: ";
    std::getline(std::wcin, searchPublisher);

    std::wcout << L"Введіть рік для пошуку журналів після цього року: ";
    std::wcin >> searchYear;

    printByPublisher(magazines, searchPublisher);
    printAfterYear(magazines, searchYear);

    return 0;
}
