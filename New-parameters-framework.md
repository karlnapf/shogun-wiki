Tag<int> intParameter;

object.set(intParameter, 3)

template <typename T>
void set(Tag<T> tag, T value)

template <typename T>
void set(string name, T value)

T = int/double/ CKernel/CClassifier/

CKernel* shogun.kernel("gaussian")

object.set("non-int parameter", int, double, CKernel,);

# RuntimeError: parameters are blablabla, width,







shogun.kernel.gaussian

kernel = shogun.kernel("gaussian");
#kernel.set("width", shogun.range.exponential(-5.0, 5.0));
#kernel.set("width", shogun.prior.uniform(0, 1));
#kernel.set("width", shogun.just(3));
other_kernel = shogun.kernel("linear");

kernel.parameter("width").is(shogun.range());

svm = shogun.classifier("libsvm");
svm.set("kernel", shogun.any_of(kernel, other_kernel));
svm.train();


class SGObject {
    unordered_map<Tag, Parameter> parameters;

    template <T>
    void uses(string name) {
        parameters[Tag<T>(name)] = new parameter
    }

}

static Tag<CKernel> KERNEL("kernel");
static Tag<float> KERNEL_WIDTH("width");

class LibSVM {
    LibSVM() : Object() {
        uses<int>("max_iterations");
    }

    void train() {
        get(KERNEL).get(KERNEL_WIDTH);
    }
}