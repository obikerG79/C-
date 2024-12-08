#include <iostream>
#include <windows.h> 

// Данные дерева
const int TREE_SIZE = 15;
const int treeValues[TREE_SIZE + 1] = {0, 10, 22, 16, 11, 45, 25, 25, 4, 10, 7, 8, 25, 10, 1, 9};

// Функция для вычисления суммы чисел-пометок всех вершин
int calculateSum(int node) {
    if (node > TREE_SIZE) {
        return 0; // Если вершина отсутствует
    }
    return treeValues[node] + calculateSum(2 * node) + calculateSum(2 * node + 1);
}

// Функция для вычисления суммы чисел-пометок, превышающих 15
int calculateSumGreaterThan(int node, int limit) {
    if (node > TREE_SIZE) {
        return 0; // Если вершина отсутствует
    }
    int current = (treeValues[node] > limit) ? treeValues[node] : 0;
    return current + calculateSumGreaterThan(2 * node, limit) + calculateSumGreaterThan(2 * node + 1, limit);
}

// Рекурсивный обход для вывода номеров вершин с числом-пометкой > 15
void printNodesGreaterThan(int node, int limit) {
    if (node > TREE_SIZE) {
        return; // Если вершина отсутствует
    }
    if (treeValues[node] > limit) {
        std::cout << node << " ";
    }
    printNodesGreaterThan(2 * node, limit);
    printNodesGreaterThan(2 * node + 1, limit);
}

int main() {
    // Устанавливаем кодировку консоли UTF-8
    SetConsoleCP(65001);
    SetConsoleOutputCP(65001);

    std::cout << "Дерево с числами-пометками: ";
    for (int i = 1; i <= TREE_SIZE; ++i) {
        std::cout << treeValues[i] << " ";
    }
    std::cout << std::endl;

    // 1. Сумма чисел-пометок всех вершин
    int totalSum = calculateSum(1);
    std::cout << "Сумма чисел-пометок всех вершин: " << totalSum << std::endl;

    // 2. Сумма чисел-пометок, превышающих 15
    int sumGreaterThan15 = calculateSumGreaterThan(1, 15);
    std::cout << "Сумма чисел-пометок вершин, превышающих 15: " << sumGreaterThan15 << std::endl;

    // 3. Вывод номеров вершин с числом-пометкой > 15
    std::cout << "Номера вершин с числом-пометкой > 15: ";
    printNodesGreaterThan(1, 15);
    std::cout << std::endl;

    // Пауза перед завершением программы
    std::cout << "Нажмите Enter для завершения программы..." << std::endl;
    std::cin.ignore();
    std::cin.get();

    return 0;
}
