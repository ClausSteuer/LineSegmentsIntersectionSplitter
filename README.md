# LineSegmentsIntersectionSplitter

Calculates the intersections of a set of line segments and splits the line segments at their intersections.
Implements a modified version of the Bentley–Ottmann algorithm described in [de Berg, Mark, et al. Computational Geometry: Algorithms and Applications (2008)](http://link.springer.com/book/10.1007/978-3-540-77974-2).

## Dependencies

Requires gcc 4.7+ or clang 3.1+, gmock 1.7+ for building the tests (optional) and doxygen for generating the documentatíon (also optional).

## How to build

In the project root run:
~~~~~~~~~~~~~{.txt}
mkdir build
cd build
cmake ..
make
~~~~~~~~~~~~~
To install the library at the location defined by the `CMAKE_INSTALL_PREFIX` variable run `make install` inside the `build` directory.

Set `STATIC_INTERSECTIONSPLITTER=ON` to build a static library (shared by default).

Run `make doc` to generate the documentation (doxygen must be installed and and found by cmake).

### Build and run the tests

For building the tests checkout [gmock (>= 1.7)](https://code.google.com/p/googlemock/source/checkout) into `<project-root>/gmock` and set the cmake variable `BUILD_TESTS=ON`:

~~~~~~~~~~~~~{.txt}
svn checkout http://googlemock.googlecode.com/svn/tags/release-1.7.0 gmock
cmake .. -DBUILD_TESTS=ON
./intersectionsplitter/tests/intersectionsplitter-tests
~~~~~~~~~~~~~

## How to use

~~~~~~~~~~~~~{.cpp}
#include <intersectionsplitter/IntersectionSplitter.h>
#include <intersectionsplitter/PrintUtils.h>

int main(int, char**) {

    std::vector<intersectionsplitter::LineSegmentPtr> input = {
        intersectionsplitter::LineSegment::create(0,2, 4,2),
        intersectionsplitter::LineSegment::create(2,4, 2,0)
    };

    std::cout << "Splitting: " << std::endl << input << std::endl;

    std::vector<LineSegmentPtr> result = intersectionsplitter::splitLineSegmentsAtIntersections(input);

    std::cout << "Result: " << std::endl << result;

    return 0;

}

~~~~~~~~~~~~~

Output:
~~~~~~~~~~~~~{.txt}
Splitting:
[s: (0, 2), e: (4, 2), len: 4]
[s: (2, 4), e: (2, 0), len: 4]

Result:
[s: (2, 2), e: (2, 0), len: 2]
[s: (2, 2), e: (4, 2), len: 2]
[s: (2, 4), e: (2, 2), len: 2]
[s: (0, 2), e: (2, 2), len: 2]
~~~~~~~~~~~~~
