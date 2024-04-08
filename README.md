#include <iostream>
#include <string>
#include <sstream>
#include <cctype>
// Функція для підрахунку кількості чисел у тексті
int countNumbers(const std::string& text) {
    int count = 0;
    std::istringstream iss(text);
    std::string word;
    while (iss >> word) {
        bool isNumber = true;
        for (char c : word) {
            if (!std::isdigit(c)) {
                isNumber = false;
                break;
            }
        }
        if (isNumber) {
            count++;
        }
    }
    return count;
}
// Функція для переведення числа у текст
std::string numberToWords(const std::string& price) {
    std::string result;
    std::istringstream iss(price);
    int dollars, cents;
    char comma;
    iss >> dollars >> comma >> cents;
    static const std::string ones[] = {"", "одна", "дві", "три", "чотири", "п'ять", "шість", "сім", "вісім", "дев'ять"};
    static const std::string teens[] = {"десять", "одинадцять", "дванадцять", "тринадцять", "чотирнадцять", "п'ятнадцять", "шістнадцять", "сімнадцять", "вісімнадцять", "дев'ятнадцять"};
    static const std::string tens[] = {"", "десять", "двадцять", "тридцять", "сорок", "п'ятдесят", "шістдесят", "сімдесят", "вісімдесят", "дев'яносто"};
    static const std::string hundreds[] = {"", "сто", "двісті", "триста", "чотириста", "п'ятсот", "шістсот", "сімсот", "вісімсот", "дев'ятсот"};
    if (dollars >= 0 && dollars < 1000) {
        result += hundreds[dollars / 100] + " " + tens[(dollars % 100) / 10] + " " + ones[dollars % 10] + " гривень ";
    }
    if (cents >= 0 && cents < 100) {
        result += tens[cents / 10] + " " + ones[cents % 10] + " копійок";
    }
    return result;
}
// Функція для виведення на екран слів, що складаються тільки з латинських літер
void printLatinWords(const std::string& text) {
    std::istringstream iss(text);
    std::string word;
    while (iss >> word) {
        bool allLatin = true;
        for (char c : word) {
            if (!std::isalpha(c) || !std::islower(c)) {
                allLatin = false;
                break;
            }
        }
        if (allLatin) {
            std::cout << word << std::endl;
        }
    }
}
int main() {
    // Завдання 1: підрахунок кількості чисел у тексті
    std::string text;
    std::cout << "Введіть текст: ";
    std::getline(std::cin, text);
    int numberCount = countNumbers(text);
    std::cout << "Кількість чисел у тексті: " << numberCount << std::endl;
    // Завдання 2: переведення вартості товару у текст
    std::string price;
    std::cout << "Введіть вартість товару (у форматі дол.цент): ";
    std::getline(std::cin, price);
    std::string textPrice = numberToWords(price);
    std::cout << "Вартість товару словами: " << textPrice << std::endl;
    // Завдання 3: виведення слів, що складаються тільки з латинських літер
    std::cout << "Слова, що складаються тільки з латинських літер:" << std::endl;
    printLatinWords(text);
    return 0;
}
