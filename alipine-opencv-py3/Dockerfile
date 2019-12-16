FROM alpine-opencv-py3-builder as builder

FROM alpine:3.10.3

# install depndency 
RUN apk add --update --no-cache python3 openblas musl libgcc

# NOTE: maybe builder is symbolic link, but target isn't symbolic link, it's full size library(.so) copy
# copy opencv lib
COPY --from=builder /usr/lib64/libopencv_imgcodecs.so.4.1 /usr/lib64/
COPY --from=builder /usr/lib64/libopencv_imgproc.so.4.1 /usr/lib64/
COPY --from=builder /usr/lib64/libopencv_core.so.4.1 /usr/lib64/
# copy depndency 
COPY --from=builder /usr/lib/libstdc++.so.6 /usr/lib/
COPY --from=builder /usr/lib/libjpeg.so.8 /usr/lib/
COPY --from=builder /usr/lib/libpng16.so.16 /usr/lib/
COPY --from=builder /usr/lib/libwebp.so.7 /usr/lib/
COPY --from=builder /usr/lib/libjasper.so.4 /usr/lib/
COPY --from=builder /lib/libz.so.1 /lib/
COPY --from=builder /usr/lib/python3.7/site-packages/numpy/ /usr/lib/python3.7/site-packages/numpy/
# copy opencv for python import 
COPY --from=builder /usr/lib/python3.7/site-packages/cv2/python-3.7/cv2.cpython-37m-x86_64-linux-gnu.so /usr/lib/python3.7/site-packages/cv2.so

# link
RUN ln -vfs /usr/bin/python3 /usr/local/bin/python && \
    ln -vfs /usr/bin/pip3 /usr/local/bin/pip

# for debug usage
RUN apk add bash bash-completion lddtree

WORKDIR /app

CMD ["python"]