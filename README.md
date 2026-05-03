# git-commit-analiz

#include <iostream>
#include <vector>

// Basit bir bellek buffer yonetimi ornegi
class DataBuffer {
public:
    // KOTU PRATIK: Ham pointer kullanimi (AI bunu yakalamali)
    int* buffer;
    int size;

    DataBuffer(int s) {
        size = s;
        buffer = new int[size]; 
        std::cout << "Buffer olusturuldu, boyut: " << size << std::endl;
    }

    // HATA: Destructor s.eksik.!(Memory leak - AI bunu kesinlikle raporlamali)
    // ~DataBuffer() { delete[] buffer; }

    void writeData(int index, int value) {
        // GUVENLIK ACIGI: Out of bounds kontrolu yok
        buffer[index] = value;
    }

    void printBuffer() {
        for (int i = 0; i < size; i++) {
            std::cout << buffer[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    DataBuffer myBuf(5);
    myBuf.writeData(0, 100);
    myBuf.writeData(1, 200);
    
    // AI buradaki tehlikeyi fark  edecektir.
    myBuf.writeData(10, 500); 

    myBuf.printBuffer();
    return 0;
}
