  int arr[] = { 4,6,2,2,1,6,9,9,10,10 ,9,4};
    int n = sizeof(arr) / sizeof(int);
    
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (arr[i] == arr[j] && j != i) {
                arr[j] = arr[j + 1];
                
                n--;
            }
        }
    }
    
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    
    return 0;
