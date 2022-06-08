package coverage

import (
	"fmt"
	"os"
	"reflect"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func createBirthday(month time.Month, day, year int) time.Time {
	return time.Date(year, month, day, 0, 0, 0, 0, time.Local)
}

func getPeople() People {
	return People{
		{firstName: "Ihor", lastName: "Ost", birthDay: createBirthday(1, 3, 1986)},
		{firstName: "A", lastName: "A", birthDay: createBirthday(6, 20, 2017)},
		{firstName: "A", lastName: "B", birthDay: createBirthday(6, 20, 2017)},
		{firstName: "B", lastName: "B", birthDay: createBirthday(6, 20, 2017)},
	}
}

func TestPeople_Len(t *testing.T) {
	got := getPeople().Len()
	want := 4
	if got != want {
		t.Errorf("Len() = %v, want %v", got, want)
	}
}

func TestPeople_Less(t *testing.T) {
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want bool
	}{
		{
			name: "should return false for older person",
			p:    getPeople(),
			args: args{0, 1},
			want: false,
		}, {
			name: "should return true for lastName A < B",
			p:    getPeople(),
			args: args{1, 2},
			want: true,
		},
		{
			name: "should return true for firstName A < B",
			p:    getPeople(),
			args: args{2, 3},
			want: true,
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Less(tt.args.i, tt.args.j); got != tt.want {
				t.Errorf("Less() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	p := getPeople()
	p.Swap(0, 1)
	got := p[0].firstName
	want := "A"
	if got != want {
		t.Errorf("The first person after swap should be %v, but got %v", want, got)
	}
}

// Matrix

func TestNew(t *testing.T) {
	tests := []struct {
		name string
		ms   string
		want *Matrix
		err  error
	}{
		{
			name: "wrong row len",
			ms:   "1 1 1\n1 1",
			want: nil,
			err:  fmt.Errorf("Rows need to be the same length"),
		}, {
			name: "wrong matrix element type",
			ms:   "1 1 1\n1 1 a",
			want: nil,
			err:  fmt.Errorf("strconv.Atoi: parsing \"a\": invalid syntax"),
		}, {
			name: "new matrix returned",
			ms:   "1 1 1\n1 1 1",
			want: &Matrix{rows: 2, cols: 3, data: []int{1, 1, 1, 1, 1, 1}},
			err:  nil,
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			got, err := New(tt.ms)
			if err != nil && err.Error() != tt.err.Error() {
				t.Errorf("Expected to get err %v, but got %v", tt.err, err)
			}
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("Expected to get %v, but got %v", tt.want, got)
			}
		})
	}
}

func TestMatrix_Rows(t *testing.T) {
	m, err := New("1 2 3\n1 2 3\n1 2 3")
	if err != nil {
		t.Errorf("expected to get matrix but got error %v", err)
	}
	got := m.Rows()
	want := [][]int{
		{1, 2, 3},
		{1, 2, 3},
		{1, 2, 3},
	}
	if !reflect.DeepEqual(got, want) {
		t.Errorf("Expected to get %v, but got %v", want, got)
	}
}

func TestMatrix_Cols(t *testing.T) {
	m, err := New("1 2 3\n1 2 3\n1 2 3")
	if err != nil {
		t.Errorf("expected to get matrix but got error %v", err)
	}
	got := m.Cols()
	want := [][]int{
		{1, 1, 1},
		{2, 2, 2},
		{3, 3, 3},
	}
	if !reflect.DeepEqual(got, want) {
		t.Errorf("Expected to get %v, but got %v", want, got)
	}
}

func TestMatrix_Set(t *testing.T) {
	m, err := New("1 2 3\n1 2 3\n1 2 3")
	if err != nil {
		t.Errorf("expected to get matrix but got error %v", err)
	}
	tests := []struct {
		name string
		args [2]int
		want bool
	}{
		{name: "should set value", args: [2]int{0, 0}, want: true},
		{name: "should not set value for 4th row", args: [2]int{4, 0}, want: false},
		{name: "should not set value for 4th col", args: [2]int{0, 4}, want: false},
	}

	for _, tt := range tests {
		got := m.Set(tt.args[0], tt.args[1], 0)
		if got != tt.want {
			t.Errorf("Expected to get %v, but got %v", tt.want, got)
		}
	}
}
