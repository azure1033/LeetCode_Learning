# Quick Sort
## Introduction
> 快速排序是C·A·R·Hoare发明的排序算法.在平均情况下,它的时间复杂度是O(nlogn),最差情况下时间复杂度为O(n^2).

## Algorithm
- 选择一个元素作为基准值pivot**_一般会取第一个元素_**.
- 左右指针遍历除pivot以外的数组元素,将比pivot小的元素放在左边,大的元素放在右边.具体来说,对于左指针,如果遇到比pivot小(**或等于**)的元素,就将左指针右移,否则就停止处理右指针;对于右指针,如果遇到比pivot大(**或等于**)的元素,就将右指针左移,否则就停止并将左右指针的值交换,重复上述过程,直到左指针大于右指针.
- 上述过程结束后,将pivot与右侧指针交换.**显然在遍历完后,右侧指针指向第一个小于pivot的元素,这个位置正是我们想要找到的Pivot的位置**.
- 递归地对右指针(**即pivot的位置**)左侧和右侧进行QS.就可以得到我们要的结果.
  
``` C++
int partition(std::vector<int>& nums, int first, int last)
{
  int pivot = nums[first];
  int left = first + 1;
  int right = last;
  while (left <= right)
  {
    while (left <= right && nums[left] <= pivot)
        left++;
    while (left <= right && nums[right] >= pivot)
        right--;
    if (left < right) std::swap(nums[left], nums[right]) 
  }
  std::swap(nums[first], nums[right]);
  return right;
}

void quickSort(std::vector<int>& nums, int first, int last)
{
  if (first < last)
  {
    int splitpoint = partition(nums, first, last);
    quickSort(nums, first, splitpoint - 1);
    quickSort(nums, splitpoint + 1, last);
  }
}
```

